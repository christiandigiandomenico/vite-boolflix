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

        starVote() {
            const vote = Math.round(this.series.vote_average / 2);
            const arrayStars = ['fa-regular fa-star', 'fa-regular fa-star', 'fa-regular fa-star', 'fa-regular fa-star', 'fa-regular fa-star'];
            for(let i = 0; i < vote; i++ ) {
                arrayStars.pop();
                arrayStars.unshift('fa-solid fa-star');
            }
            return arrayStars;
        },

    },

}

</script>

<template>

    <!--<li class="series">-->
        <!--<img :src="getSeriesUrl(series.poster_path)" :alt="series.original_title">-->
        <!--<span class="card-title">{{ series.name }}</span>-->
        <!--<span class="card-original-title">{{ series.original_name }}</span>-->
        <!--<span class="card-language"><img :src="getFlagSeriesUrl(series.original_language)"></span>-->
        <!--<div class="star-vote-series"><i v-for="star in starVote()" :class="star"></i></div>-->
    <!--</li> -->

    <li class="series">

    <div class="flip-card">
        <div class="flip-card-inner">
            <div class="flip-card-front">
                <img :src="getSeriesUrl(series.poster_path)" :alt="series.original_title">
            </div>
        <div class="flip-card-back">
            <span class="card-title">{{ series.name }}</span>
            <span class="card-original-title">{{ series.original_name }}</span>
            <span class="card-language"><img :src="getFlagSeriesUrl(series.original_language)"></span>
            <span class="card-original-title">{{ series.overview }}</span>
            <div class="star-vote"><i v-for="star in starVote()" :class="star"></i></div>
        </div>
    </div>

    </div>
    </li>

</template>

<style lang="scss">

.flip-card {
  background-color: transparent;
  width: 300px;
  height: 500px;
  border: 1px solid #f1f1f1;
  perspective: 1000px;
}

.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}

.flip-card:hover .flip-card-inner {
  transform: rotateY(180deg);
}

.flip-card-front, .flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
}

.flip-card-front {
  background-color: #bbb;
  color: black;
}

.flip-card-back {
  background-color: gray;
  color: white;
  transform: rotateY(180deg);
}

.series {
    display: flex;
    flex-direction: column;

    padding: 20px;

    width: calc(100% / 5);
    .star-vote {
        display: flex;
    }
    img {
        width: 100%;
        height: 100%;
    }
    .flip-card-back {

        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;

        .card-original-title {
            margin-bottom: 20px;
        }

        img {
        width: 20px;
        height: 20px;
    }

    }
    
}

</style>