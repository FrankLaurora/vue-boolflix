<template>
    <header>
        <input type="text" v-model="titleSearch" @keyup.enter.prevent="fetchMovies(titleSearch); $emit('searchByTitle', movieList)">
        <button @click.prevent="fetchMovies(titleSearch); $emit('searchByTitle', movieList)">Cerca</button>
    </header>
</template>

<script>
import axios from 'axios';

export default {
    name: 'Header',

    data() {
        return {
            titleSearch: "",
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

<style lang="scss" scoped>
 
</style>