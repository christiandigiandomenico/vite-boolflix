<script>
export default {
    name: 'AppCard',

    props: {
        movie: Object,
        cast: Array,
        genres: Array,
    },

    methods: {

        getGenresName() {
                if (this.movie.genre_ids && this.genres.length > 0) {
                        const genreNames = this.movie.genre_ids.map(genreId => {
                            const genre = this.genres.find(genre => genre.id === genreId);
                            return genre ? genre.name : '';
                        });
                        return genreNames.join(', ');
                    } else {
                        return '';
                    }
            },

        getFlagUrl(language) {

            let flag = this.movie.original_language

            switch(this.movie.original_language){
            case "ja":
                flag = "jp";
                break;
            case "en":
                flag = "us";
                break;
            case "ko":
                flag = "kr";
                break;
            case "da":
                flag = "dk";
                break;
            case "zh":
                flag = "cn";
                break;
            case "cs":
                flag = "cz"
                break;
            case "uk":
                flag = "gb"
                break;
            case "hi":
                flag = "in"
                break;
            case "sv":
                flag = "se"
                break;
            default:
            }

            return `https://flagcdn.com/16x12/${flag}.png`;
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
            }
            return arrayStars;
        },

        getCastNames() {
            if(this.cast && this.cast.length) {
                let castNames = '';
                const maxMember = 5;
                for (let i = 0; i < Math.min(this.cast.length, maxMember); i++) {
                    castNames += this.cast[i].name;
                    if (i < Math.min(this.cast.length, maxMember) - 1) {
                        castNames += ', ';
                    }
                } return castNames;
            } else {
            return '';
        }
        },

    },
}
</script>

<template>
    <!--<li class="movie">-->
        <!--<img :src="getImageUrl(movie.poster_path)" :alt="movie.original_title">-->
        <!--<span class="card-title">{{ movie.title }}</span>-->
        <!--<span class="card-original-title">{{ movie.original_title }}</span>-->
        <!--<span class="card-language"><img :src="getFlagUrl(movie.original_language)"></span>-->
        <!--<span class="card-vote">{{ movie.vote_average }}</span>-->
        <!--<div class="star-vote"><i v-for="star in starVote()" :class="star"></i></div>-->
    <!--</li>-->

    <li class="movie">

        <div class="flip-card">
            <div class="flip-card-inner">
                <div class="flip-card-front">
                    <img :src="getImageUrl(movie.poster_path)" :alt="movie.original_title">
                </div>
            <div class="flip-card-back">
                <span class="card-title">{{ movie.title ? movie.title : movie.name}}</span>
                <span class="card-original-title">{{ movie.original_title ? movie.original_title : movie.original_name }}</span>
                <span class="card-language"><img :src="getFlagUrl(movie.original_language)"></span>
                <span class="card-original-title">{{ movie.overview }}</span>
                <!--<span class="card-vote">{{ movie.vote_average }}</span>-->
                <div class="star-vote"><i v-for="star in starVote()" :class="star"></i></div>
                <div class="cast-members" v-if="cast && cast.length"><strong>Cast:</strong> {{ getCastNames() }}</div>
                <div v-if="getGenresName()"><span>Generi: </span>{{ getGenresName() }}</div>
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
  overflow-y: auto;
}

.movie {
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
        object-fit: cover;
    }
    .flip-card-back {

        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;

        .star-vote{
            margin-bottom: 10px;
            i {
                color: rgb(255, 196, 0);
            }
        }

        .card-title {
            font-size: 24px;
            font-weight: bold;
        }

        .card-original-title {
            margin-bottom: 20px;
        }

        img {
        width: 20px;
        height: 15px;
    }

    }
    
}

</style>