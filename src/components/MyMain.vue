<template>
    <main>
        <h1>Film:</h1>
        <div class="container">
            <div class="card" v-for="(movie, index) in moviesSearchResults" v-bind:key="index">
                <div>Poster: <img v-bind:src="posterUrl + movie.poster_path" v-bind:alt="movie.title" /></div>
                <p>Titolo: {{movie.title}}</p>
                <p>Titolo originale: {{movie.original_title}}</p>
                <p>Lingua originale: <img class="flag" v-bind:src="changeStringToFlag(movie.original_language)" v-bind:alt="movie.original_language" /></p>
                <p>Media voto: {{movie.vote_average}}</p>
                <p>Media voto: {{getIntegerVote(movie.vote_average)}}</p>
            </div>
        </div>
        <h1>Serie TV:</h1>
        <div class="container">
            <div class="card" v-for="(serie, index) in seriesSearchResults" v-bind:key="index">
                <div>Poster: <img v-bind:src="posterUrl + serie.poster_path" v-bind:alt="serie.name" /></div>
                <p>Titolo: {{serie.name}}</p>
                <p>Titolo originale: {{serie.original_name}}</p>
                <p>Lingua originale: <img class="flag" v-bind:src="changeStringToFlag(serie.original_language)" v-bind:alt="serie.original_language" /></p>
                <p>Media voto: {{serie.vote_average}}</p>
                <p>Media voto: {{getIntegerVote(serie.vote_average)}}</p>
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
            posterUrl: 'https://image.tmdb.org/t/p/w185' // dopo inserire w342
        }
    },
    methods: {
        changeStringToFlag(languageString) {
            let imgSrc = '';
            if (languageString == 'de' || languageString == 'en' || languageString == 'es' || languageString == 'fr' || languageString == 'it') {
                imgSrc = require(`../assets/flags/${languageString}.png`);
            } else {
                imgSrc = languageString;
            }
            return imgSrc;
        },
        getIntegerVote(vote) {
            let newVote = Math.round(vote / 2);
            return newVote;
        }
    }
}
</script>

<style lang='scss'>
@import '../styles/vars.scss';

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
            padding: 10px;
            flex-basis: calc(100% / 5 - 4px);
            margin-top: 4px;
            color: #fff;
            border: 1px solid $bg_c1;
            background-color: grey;

            .flag {
                max-width: 20px;
            }
        }
    }
}

</style>