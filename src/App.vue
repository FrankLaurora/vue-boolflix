<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <Header @searchByTitle="fetchMovies"/>
    <Catalogue :userSearch="movieList"/>
  </div>
</template>

<script>
import Catalogue from './components/Catalogue.vue';
import Header from './components/Header.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    Header,
    Catalogue
  },

  data() {
    return {
      movieList: []
    }
  },

  methods: {
    fetchMovies(titleSearch) {
        axios.get('https://api.themoviedb.org/3/search/movie', {
                params: {
                    api_key: '1d2064f2ac36d63f2852970763f815fc',
                    query: titleSearch
                }
            })
        .then(
            (response) => {
                console.log(response);
                this.movieList = response.data.results;
            }
        );

        return this.movieList;
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
