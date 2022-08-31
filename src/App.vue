<template>
  <div id="app">
    <MyHeader @searchThis='getWordsToSearch' />
    <MyMain />
  </div>
</template>

<script>
import MyHeader from './components/MyHeader.vue';
import MyMain from './components/MyMain.vue';

export default {
  name: 'App',
  components: {
    MyHeader,
    MyMain
  },
  data() {
    return {
      wordsToSearch: ''
    }
  },
  methods: {
    getWordsToSearch(words) {
      this.wordsToSearch = words;
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
