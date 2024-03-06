<script>

import {store} from '../store.js';

export default {

name: "AppNav",

data() {
    return {

      store,
      
    }
  },

}

</script>

<template>

    <nav>

        <div class="nav-left">
            <img src="../../public/img/netflix-logo.png">

            <span>Home</span>

            <span>Serie Tv</span>

            <span>Film</span>

            <span>Originali</span>

            <span>Aggiunti di recente</span>

            <span>La mia lista</span>
        </div>

        <div class="nav-right">

            <div id="search-bar">
                <input type="search" name="saerchText" placeholder="Cerca" v-model="this.store.searchMovie">
                <button @click="$emit('search')" class="btn">Cerca</button>
            </div>

            <i class="fa-solid fa-bell"></i>

            <img src="../../public/img/netflix-avatar.png">

            &#129171;

        </div>

    </nav>
  
</template>

<style lang="scss">

nav {

    display: flex;
    justify-content: space-between;
    align-items: center;

    height: 100px;
    background-color: black;

    .nav-left {
        display: flex;
        align-items: center;
        gap: 20px;
        img {
            width: 150px;
            height: 75px;
        }
    }

    .nav-right {
        display: flex;
        align-items: center;
        gap: 20px;
        margin-right: 20px;
        #search-bar {
            .btn {
                color: black;
            }
        }
        img {
            width: 50px;
            height: 50px;
        }
    }

}

</style>
