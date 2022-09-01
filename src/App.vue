<template>
  <div id="app">
    <MyHeader @searchThis='getWordsToSearch' />
    <MyMain :searchResults='moviesList' />
  </div>
</template>

<script>
import MyHeader from './components/MyHeader.vue';
import MyMain from './components/MyMain.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    MyHeader,
    MyMain
  },
  data() {
    return {
      wordsToSearch: '',
      apiUrl: 'https://api.themoviedb.org/3/',
      myApiKey: '3642ddadc741136c1c6eda46fa6ee412',
      language: 'it-IT',
      moviesList: [],
      seriesList: []
    }
  },
  methods: {
    getWordsToSearch(words) {
      this.wordsToSearch = words;
      this.callApiMovies();
      this.callApiSeries();
    },
    callApiMovies() {
      axios.get(`${this.apiUrl}search/movie?api_key=${this.myApiKey}&language=${this.language}&query=${this.wordsToSearch}`)
      .then(response => {
        this.moviesList = response.data.results;
      })
      .catch(error => {
        console.log(error);
      })
    },
    callApiSeries() {
      axios.get(`${this.apiUrl}search/tv?api_key=${this.myApiKey}&language=${this.language}&query=${this.wordsToSearch}`)
      .then(response => {
        this.seriesList = response.data.results;
      })
      .catch(error => {
        console.log(error);
      })
    }    
  }
}
</script>

<style lang="scss">
@import './styles/general.scss';

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>