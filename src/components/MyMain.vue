<template>
    <main>
        <h1>Film:</h1>
        <div class="container flip-card">
            <div class="card flip-card-inner" v-for="(movie, index) in moviesSearchResults" v-bind:key="index">
                <div class="flip-card-front">
                    <div>Poster: <img v-bind:src="posterUrl + movie.poster_path" v-bind:alt="movie.title"></div>
                </div>
                <div class="flip-card-back">
                    <p>Titolo: {{movie.title}}</p>
                    <p>Titolo originale: {{movie.original_title}}</p>
                    <p>Lingua originale: <img class="flag" v-bind:src="changeStringToFlag(movie.original_language)" v-bind:alt="movie.original_language" /></p>
                    <p>Media voto: {{getIntegerVote(movie.vote_average)}} - <span v-for="(singleVote, index) in getIntegerVote(movie.vote_average)" :key='index'><i class="fa-solid fa-star"></i></span></p>
                </div>
            </div>
        </div>



        <h1>Serie TV:</h1>
        <div class="container">
            <div class="card" v-for="(serie, index) in seriesSearchResults" v-bind:key="index">
                <div>Poster: <img v-bind:src="posterUrl + serie.poster_path" v-bind:alt="serie.name" /></div>
                <p>Titolo: {{serie.name}}</p>
                <p>Titolo originale: {{serie.original_name}}</p>
                <p>Lingua originale: <img class="flag" v-bind:src="changeStringToFlag(serie.original_language)" v-bind:alt="serie.original_language" /></p>
                <p>Media voto: {{getIntegerVote(serie.vote_average)}} - <span v-for="(singleVote, index) in getIntegerVote(serie.vote_average)" :key='index'><i class="fa-solid fa-star"></i></span></p>
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
        /* This container is needed to position the front and back side */
        .flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;

  /* Position the front and back side */
.flip-card-front, .flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden; /* Safari */
  backface-visibility: hidden;
}
/* Style the front side (fallback if image is missing) */

.flip-card-front {
  background-color: #bbb;
  color: black;
}
/* Style the back side */

.flip-card-back {
  background-color: dodgerblue;
  color: white;
  transform: rotateY(180deg);
}
}
    }

    /* The flip card container - set the width and height to whatever you want. We have added the border property to demonstrate that the flip itself goes out of the box on hover (remove perspective if you don't want the 3D effect */
.flip-card {
  background-color: transparent;
  width: 300px;
  height: 200px;
  border: 1px solid #f1f1f1;
  perspective: 1000px; /* Remove this if you don't want the 3D effect */
}

/* Do an horizontal flip when you move the mouse over the flip box container */
.flip-card:hover .flip-card-inner {
  transform: rotateY(180deg);
}

}

</style>