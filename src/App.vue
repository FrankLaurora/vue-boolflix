<template>
  <div id="app">
    <Header @searchByTitle="fetchMovies"/>
    <Catalogue :movieSearch="movieList" :seriesSearch="seriesList"/>
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
      movieList: [],

      seriesList: []
    }
  },

  methods: {
    fetchMovies(titleSearch) {
        axios.get('https://api.themoviedb.org/3/search/movie', {
                params: {
                    api_key: '1d2064f2ac36d63f2852970763f815fc',
                    query: titleSearch,
                    language: 'it-IT'
                }
            })
        .then(
            (response) => {
                this.movieList = response.data.results;
            }
        );

        axios.get('https://api.themoviedb.org/3/search/tv', {
                params: {
                    api_key: '1d2064f2ac36d63f2852970763f815fc',
                    query: titleSearch,
                    language: 'it-IT'
                }
            })
        .then(
            (response) => {
                this.seriesList = response.data.results;
            }
        );
      }   
    }
}
</script>

<style lang="scss">
@import './assets/style/common.scss';
@import './assets/style/variables.scss';

  #app {
    background-color: $primary-color;
    min-height: 100vh;
    padding-top: $header-height;
  }

</style>
