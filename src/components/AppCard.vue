<script>
export default {
    name: 'AppCard',

    props: {
        movie: Object,
    },
}
</script>

<template>
    <li class="movie">
        <img :src="'https://' + movie.poster_path" :alt="movie.original_title">
        <span class="card-title">{{ movie.title }}</span>
        <span class="card-original-title">{{ movie.original_title }}</span>
        <span class="card-language">{{ movie.original_language }}</span>
        <span class="card-original-title">{{ movie.vote_average }}</span>
    </li>
</template>

<style lang="scss">

.movie {
    display: flex;
    flex-direction: column;

    width: calc(100% / 5);
}

</style>