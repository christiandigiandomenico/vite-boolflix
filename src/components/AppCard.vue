<script>
export default {
    name: 'AppCard',

    props: {
        movie: Object,
    },

    methods: {
        getFlagUrl(language) {
            return `https://flagcdn.com/16x12/${language.toLowerCase()}.png`;
        },

        getImageUrl(image) {
            return `https://image.tmdb.org/t/p/w1280/${image}.jpg`;
        },

        starVote() {
            const vote = Math.round(this.movie.vote_average / 2);
            const arrayStars = ['fa-regular fa-star', 'fa-regular fa-star', 'fa-regular fa-star', 'fa-regular fa-star', 'fa-regular fa-star'];
            for(let i = 0; i < vote; i++ ) {
                arrayStars.pop();
                arrayStars.unshift('fa-solid fa-star');
                console.log(arrayStars)
            }
            return arrayStars;
        }
    },
}
</script>

<template>
    <li class="movie">
        <img :src="getImageUrl(movie.poster_path)" :alt="movie.original_title">
        <span class="card-title">{{ movie.title }}</span>
        <span class="card-original-title">{{ movie.original_title }}</span>
        <span class="card-language"><img :src="getFlagUrl(movie.original_language)"></span>
        <!--<span class="card-vote">{{ movie.vote_average }}</span>-->
        <div class="star-vote"><i v-for="star in starVote()" :class="star"></i></div>
    </li>
</template>

<style lang="scss">

.movie {
    display: flex;
    flex-direction: column;

    border: 1px solid gray;
    border-radius: 25px;
    padding: 20px;

    width: calc(100% / 5);
    .star-vote {
        display: flex;
    }
}

</style>