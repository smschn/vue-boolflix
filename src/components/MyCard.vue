<template>
        <div class="card flip-card-inner">
            <div class="flip-card-front">
                <img class="poster" v-bind:src="posterUrl + data.poster_path" v-bind:alt="data.title?data.title:data.name">
            </div>
            <div class="flip-card-back">
                <h5>Titolo: {{data.title?data.title:data.name}}</h5> <!-- attenzione alla differenza tra il campo titolo tra 'movie' e 'serie'-->
                <h5>Titolo originale: {{data.original_title?data.original_title:data.original_name}}</h5> <!-- come sopra -->
                <h5>Lingua originale:
                    <img class="flag" v-if="availableFlags.includes(data.original_language)" v-bind:src="require('../assets/flags/' + data.original_language + '.png')" v-bind:alt="data.original_language">
                    <span v-else>{{data.original_language}}</span>
                </h5>
                <h5>Voto: {{getIntegerVote(data.vote_average)}}</h5>
                <span v-for="singleVote in 5" :key='singleVote'>
                    <i class="fa-star " v-bind:class=" (getIntegerVote(data.vote_average)>=singleVote)?'fa-solid':'fa-regular' "></i>
                </span>
                <h5 class="plot">Trama: {{data.overview}}</h5>
            </div>
        </div>
</template>

<script>
export default {
    name: 'MyCard',
    props: {
        data: Object
    },
    data() {
        return {
            posterUrl: 'https://image.tmdb.org/t/p/w342',
            availableFlags: ['de', 'en', 'es', 'fr', 'it']
        }
    },
    methods: {
        getIntegerVote(vote) {
            let newVote = Math.ceil(vote / 2);
            return newVote;
        }
    }
}
</script>

<style lang='scss'>
</style>