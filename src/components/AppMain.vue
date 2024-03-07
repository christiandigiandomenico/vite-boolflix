<script>

import {store} from '../store.js';

import AppCard from './AppCard.vue';
import AppSeries from './AppSeries.vue';

export default {

  name: 'AppMain',

  components: {
    AppCard,
    AppSeries,
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

    <ul>

        <AppCard v-for="currentMovie in store.movies" :movie="currentMovie"></AppCard>

        <p class="series-tv">Serie Tv</p><br>

        <br><AppSeries v-for="currentSeries in store.tvSeries" :series="currentSeries"></AppSeries>

    </ul>   

</div>

</template>

<style lang="scss">

.container {
    ul {
        display: flex;
        flex-wrap: wrap;
    }
}

</style>
