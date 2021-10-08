<template>
  <div id="app">
    <Header @searchByTitle="fetchMovies"/>
    <Catalogue :movieSearch="movieList" :seriesSearch="seriesList" :movieGenresCat="movieGenres" :tvGenresCat="tvGenres"/>
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

      seriesList: [],

      movieGenres: [],

      tvGenres: []
    }
  },

  methods: {
    fetchMovies(titleSearch) {
        // chiamata per i film
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
        // chiamata per le serie tv
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
        // chiamata per i generi dei film
        axios.get('https://api.themoviedb.org/3/genre/movie/list', {
                params: {
                    api_key: '1d2064f2ac36d63f2852970763f815fc',
                    language: 'it-IT'
                }
            })
        .then(
            (response) => {
                this.movieGenres = response.data.genres;
            }
        );
        // chiamata per i generi delle serie tv
        axios.get('https://api.themoviedb.org/3/genre/tv/list', {
                params: {
                    api_key: '1d2064f2ac36d63f2852970763f815fc',
                    language: 'it-IT'
                }
            })
        .then(
            (response) => {
                this.tvGenres = response.data.genres;
            }
        );
    }   
  },
  // al mounted effettuo una chiamata per mostrare film e serie tv popolari al caricamento della pagina
  mounted() {
      // chiamata per ottenere i film popolari
      axios.get('https://api.themoviedb.org/3/movie/popular', {
        params: {
          api_key: '1d2064f2ac36d63f2852970763f815fc',
          language: 'it-IT'
        }
      })
      .then(
            (response) => {
                this.movieList = response.data.results;
            }
      );
      // chiamata per ottenere le serie tv popolari
      axios.get('https://api.themoviedb.org/3/tv/popular', {
        params: {
          api_key: '1d2064f2ac36d63f2852970763f815fc',
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
