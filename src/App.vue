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

searchMovies() {

  axios.get('https://api.themoviedb.org/3/search/movie?api_key=417dd13ef013e66b61eb99f5ee9bd904&query=' + this.store.searchMovie)
    .then(res => {
      console.log(res.data.results)

      this.store.movies = res.data.results;
    });

    axios.get('https://api.themoviedb.org/3/search/tv?api_key=417dd13ef013e66b61eb99f5ee9bd904&query=' + this.store.searchMovie)
    .then(res2 => {
      console.log(res2.data.results)

      this.store.tvSeries = res2.data.results;
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
