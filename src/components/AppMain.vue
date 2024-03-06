<script>

import {store} from '../store.js';

import AppCard from './AppCard.vue'

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

    <ul>

        <AppCard v-for="currentMovie in store.movies" :movie="currentMovie"></AppCard>

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
