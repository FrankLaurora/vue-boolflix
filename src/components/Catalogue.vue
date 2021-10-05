<template>
    <div>
        <ul>
            <li v-for="(movie, index) in userSearch" :key="index">
                <h2>{{movie.title}}</h2>
                <h3>{{movie.original_title}}</h3>
                <h3>{{movie.original_language}}</h3>
                <h3>{{movie.vote_average}}</h3>
            </li>
        </ul>
    </div>
</template>

<script>
// import axios from 'axios'

export default {
    name: 'Catalogue',

    props: {
        userSearch: Array
    }

    // data() {
    //     return {
    //         movieList: []
    //     }
    // },

    // methods: {
    //     fetchMovies(text) {
    //         axios.get('https://api.themoviedb.org/3/search/movie', {
    //                 params: {
    //                     api_key: '1d2064f2ac36d63f2852970763f815fc',
    //                     query: text
    //                 }
    //             })
    //         .then(
    //             (response) => {
    //                 console.log(response);
    //                 this.movieList = response.data.results;
    //             }
    //         );

    //         return this.movieList;
    //     }
    // }
}
</script>

<style lang="scss" scoped>
    li{
        list-style: none;
        margin-block: 1rem;
    }

</style>