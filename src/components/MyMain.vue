<template>
    <main>
        <div class="container">
            <div class="card" v-for="(result, index) in searchResults" v-bind:key="index">
                <p>Titolo: {{result.title}}</p>
                <p>Titolo originale: {{result.original_title}}</p>
                <p>Lingua: {{result.original_language}}</p>
                <p>Media voto: {{result.vote_average}}</p> 
            </div>
        </div>
    </main>
</template>

<script>
export default {
    name: 'MyMain',
    props: {
        searchResults: Array
    }
}
</script>

<style lang='scss'>
@import '../styles/vars.scss';

main {
    height: calc(100vh - 80px);
    background-color: $bg_m;
    padding: 30px;

    .container {
        width: 90%;
        margin: auto;
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;

        .card {
            padding: 10px;
            flex-basis: calc(100% / 6 - 4px);
            margin-top: 4px;
            color: #fff;
            border: 1px solid $bg_c1;
            background-color: grey;
        }
    }
}

</style>