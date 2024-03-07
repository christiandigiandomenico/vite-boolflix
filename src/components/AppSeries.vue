<script>

import {store} from '../store.js';

export default {

  name: 'AppSeries',

  props: {
        series: Object,
    },

  data() {
        return  {
            store,
        }
    },

    methods: {

    getSeriesUrl(image) {
            return `https://image.tmdb.org/t/p/w1280/${image}.jpg`;
        },

        getFlagSeriesUrl(language) {
            return `https://flagcdn.com/16x12/${language.toLowerCase()}.png`;
        },

    },

}

</script>

<template>

    <li class="series">
        <img :src="getSeriesUrl(series.poster_path)" :alt="series.original_title">
        <span class="card-title">{{ series.title }}</span>
        <span class="card-original-title">{{ series.original_title }}</span>
        <span class="card-language"><img :src="getFlagSeriesUrl(series.original_language)"></span>
        <span class="card-original-title">{{ series.vote_average }}</span>
    </li> 

</template>

<style lang="scss">

.series {
    display: flex;
    flex-direction: column;

    width: calc(100% / 5);
}

</style>