<script>

import axios from 'axios';

import AppNav from './components/AppNav.vue';
import AppMain from './components/AppMain.vue';

import {store} from './store.js';

export default {

  data() {
    return {

      store,

    }
  },

  components: {
    AppNav,
    AppMain,
  },

  methods: {

    getGenres() {
              axios.get('https://api.themoviedb.org/3/genre/movie/list?api_key=417dd13ef013e66b61eb99f5ee9bd904').then(res => {
                this.store.filmGenres = res.data.genres;

              });

              axios.get('https://api.themoviedb.org/3/genre/tv/list?api_key=417dd13ef013e66b61eb99f5ee9bd904').then(res => {
                this.store.tvSeriesGenres = res.data.genres;

              });

          },

searchMovies() {

  axios.get('https://api.themoviedb.org/3/search/movie?api_key=417dd13ef013e66b61eb99f5ee9bd904&query=' + this.store.searchMovie)
    .then(res => {
      this.getGenres()
      console.log(res.data.results)

      this.store.movies = res.data.results;

      this.store.movies.forEach(movie => {
        axios.get(`https://api.themoviedb.org/3/movie/${movie.id}/credits?api_key=417dd13ef013e66b61eb99f5ee9bd904`).then(res => {
          this.store.castMovies[movie.id] = res.data.cast
        })
      })
    });

    axios.get('https://api.themoviedb.org/3/search/tv?api_key=417dd13ef013e66b61eb99f5ee9bd904&query=' + this.store.searchMovie)
    .then(res2 => {
      console.log(res2.data.results)

      this.store.tvSeries = res2.data.results;

      this.store.tvSeries.forEach(series => {
        axios.get(`https://api.themoviedb.org/3/tv/${series.id}/credits?api_key=417dd13ef013e66b61eb99f5ee9bd904`).then(res => {
          this.store.castSeries[series.id] = res.data.cast
        })
      })
    });

},

},

}

</script>

<template>

  <AppNav @search="searchMovies()"></AppNav>

  <AppMain></AppMain>
  
</template>

<style>

</style>
