<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <Header @searchByTitle="getTitle"/>
    <Catalogue :userSearch="userSearch"/>
  </div>
</template>

<script>
import Catalogue from './components/Catalogue.vue'
import Header from './components/Header.vue'

export default {
  name: 'App',
  components: {
    Header,
    Catalogue
  },

  data() {
    return {
      userSearch: null
    }
  },

  methods: {
    getTitle(textInput) {
      this.userSearch = textInput
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
