<script>

import {store} from '../store.js';

import AppCard from './AppCard.vue';

export default {

  name: 'AppMain',

  components: {
    AppCard,
  },

  data() {
        return  {
            store,
        }
    },

}

</script>

<template>

<div class="container">

    <div class="movie-section">Film</div>

    <ul>

        <AppCard v-for="currentMovie in store.movies" :movie="currentMovie"></AppCard>

    </ul>

    <div class="series-section">Telefilm</div>

    <ul>

        <AppCard v-for="currentSeries in store.tvSeries" :movie="currentSeries"></AppCard>

    </ul>   

</div>

</template>

<style lang="scss">

.container {
    .movie-section {
        font-size: 40px;
        font-weight: bold;
        border-bottom: 1px solid gray;
        margin-bottom: 20px;
    }
    .series-section {
        font-size: 40px;
        font-weight: bold;
        border-bottom: 1px solid gray;
        margin-bottom: 20px;
    }
    ul {
        display: flex;
        flex-wrap: wrap;
    }
}

</style>
