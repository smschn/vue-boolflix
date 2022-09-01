<template>
    <main>
        <h1 v-if="moviesSearchResults.length > 0">Film:</h1>
        <div class="container flip-card">
            <div class="card flip-card-inner" v-for="(movie, index) in moviesSearchResults" v-bind:key="index">
                <div class="flip-card-front">
                    <img v-bind:src="posterUrl + movie.poster_path" v-bind:alt="movie.title">
                </div>
                <div class="flip-card-back">
                    <h3>Titolo:</h3>
                    <p>{{movie.title}}<p>
                    <h3>Titolo originale:</h3>
                    <p>{{movie.original_title}}</p>
                    <h3>Lingua originale:</h3>
                    <img class="flag" v-if="availableFlags.includes(movie.original_language)" v-bind:src="require('../assets/flags/' + movie.original_language + '.png')" v-bind:alt="movie.original_language">
                    <span v-else>{{movie.original_language}}</span>
                    <h3>Voto:</h3>
                    <span v-for="(singleVote, index) in getIntegerVote(movie.vote_average)" :key='index'><i class="fa-solid fa-star"></i></span>
                </div>
            </div>
        </div>
        <h1 v-if="seriesSearchResults.length > 0">Serie TV:</h1>
        <div class="container flip-card">
            <div class="card flip-card-inner" v-for="(serie, index) in seriesSearchResults" v-bind:key="index">
                <div class="flip-card-front">
                    <img v-bind:src="posterUrl + serie.poster_path" v-bind:alt="serie.name">
                </div>
                <div class="flip-card-back">
                    <h3>Titolo:</h3>
                    <p>{{serie.name}}<p>
                    <h3>Titolo originale:</h3>
                    <p>{{serie.original_name}}</p>
                    <h3>Lingua originale:</h3>
                    <img class="flag" v-if="availableFlags.includes(serie.original_language)" v-bind:src="require('../assets/flags/' + serie.original_language + '.png')" v-bind:alt="serie.original_language">
                    <span v-else>{{serie.original_language}}</span>
                    <h3>Voto:</h3>
                    <span v-for="(singleVote, index) in getIntegerVote(serie.vote_average)" :key='index'><i class="fa-solid fa-star"></i></span>
                </div>
            </div>
        </div>
    </main>
</template>

<script>
export default {
    name: 'MyMain',
    props: {
        moviesSearchResults: Array,
        seriesSearchResults: Array
    },
    data() {
        return {
            posterUrl: 'https://image.tmdb.org/t/p/w342',
            availableFlags: ['de', 'en', 'es', 'fr', 'it']
        }
    },
    methods: {
        getIntegerVote(vote) {
            let newVote = Math.round(vote / 2);
            return newVote;
        }
    }
}
</script>

<style lang='scss'>
@import '../styles/vars.scss';
@import '~@fortawesome/fontawesome-free/css/all.css';

main {
    min-height: calc(100vh - 80px);
    background-color: $bg_m;
    padding: 30px;

    h1 {
        margin: 30px;
    }

    .container {
        width: 90%;
        margin: auto;
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;

        .card {
            flex-basis: calc(100% / 5);
            height: 350px;
            margin: 5px;
            color: #fff;

            .flag {
                max-width: 20px;
            }
        }

        /* This container is needed to position the front and back side */
        .flip-card-inner {
            position: relative;
            text-align: center;
            transition: transform 0.8s;
            transform-style: preserve-3d;
            
            /* Position the front and back side */
            .flip-card-front, .flip-card-back {
                position: absolute;
                -webkit-backface-visibility: hidden; /* Safari */
                backface-visibility: hidden;
            }
                
            /* Style the front side (fallback if image is missing) */
            .flip-card-front {
                color: black;

                img {
                    max-width: 100%;
                    max-height: 100%;
                }
            }

            /* Style the back side */
            .flip-card-back {
                transform: rotateY(180deg);
                width: 100%;
                height: 100%;

                h3 {
                    margin: 10px;
                }
            }
        }
        
        /* Do an horizontal flip when you move the mouse over the flip box container */
        .flip-card-inner:hover {
            transform: rotateY(180deg);
        }

    }
    
    /* The flip card container - set the width and height to whatever you want. We have added the border property to demonstrate that the flip itself goes out of the box on hover (remove perspective if you don't want the 3D effect */
    .flip-card {
        background-color: transparent;
    }

    /* Do an horizontal flip when you move the mouse over the flip box container */
    .flip-card-inner:hover {
    transform: rotateY(180deg);
    }
}
</style>