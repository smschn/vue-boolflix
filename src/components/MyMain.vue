<template>
    <main>  
        <h1 v-if="moviesSearchResults.length > 0">Film:</h1>
        <div class="container flip-card">
            <MyCard v-for="(movie, index1) in moviesSearchResults" v-bind:key="index1" :data="movie" /> <!-- Con le props invio a 'MyCard' ogni oggetto 'movie' che viene ciclato tramite 'data' -->
        </div>
        <h1 v-if="seriesSearchResults.length > 0">Serie TV:</h1>
        <div class="container flip-card">
            <MyCard v-for="(serie, index2) in seriesSearchResults" v-bind:key="index2" :data="serie" /> <!-- Con le props invio a 'MyCard' ogni oggetto 'serie' che viene ciclato tramite 'data' -->
        </div>
    </main>
</template>

<script>
import MyCard from './MyCard.vue';

export default {
    name: 'MyMain',
    components: {
        MyCard
    },
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
            let newVote = Math.ceil(vote / 2);
            return newVote;
        }
    }
}
</script>

<style lang='scss'>
@import '../styles/vars.scss';
@import '~@fortawesome/fontawesome-free/css/all.css';
@import '../styles/card.scss';

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
    }
}
</style>