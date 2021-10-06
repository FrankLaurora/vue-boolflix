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
                    query: titleSearch
                }
            })
        .then(
            (response) => {
                console.log(response);
                this.movieList = response.data.results;
            }
        );

        axios.get('https://api.themoviedb.org/3/search/tv', {
                params: {
                    api_key: '1d2064f2ac36d63f2852970763f815fc',
                    query: titleSearch
                }
            })
        .then(
            (response) => {
                console.log(response);
                this.seriesList = response.data.results;
            }
        );
      }   
    }

    // fetchSeries(titleSearch) {
    //     axios.get('https://api.themoviedb.org/3/search/tv', {
    //             params: {
    //                 api_key: '1d2064f2ac36d63f2852970763f815fc',
    //                 query: titleSearch
    //             }
    //         })
    //     .then(
    //         (response) => {
    //             console.log(response);
    //             this.seriesList = response.data.results;
    //         }
    //     );

    //     return this.seriesList;
    // }   
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
