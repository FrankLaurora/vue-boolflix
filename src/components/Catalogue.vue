<template>
    <div class="catalogue">
        <div class="container">
            <ul>
                <li v-for="element in movieSearch" :key="element.id">
                    <Card :id="element.id" :data_object="element" :genres="movieGenresCat"/>
                </li>
                <li v-for="element in seriesSearch" :key="element.id">
                    <Card :id="element.id" :data_object="element" :genres="tvGenresCat"/>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
import Card from './Card.vue';

export default {
    name: 'Catalogue',

    components: {
        Card
    },

    data() {
        return {
            id: []
        }
    },

    props: {
        movieSearch: Array,
        seriesSearch: Array,
        movieGenresCat: Array,
        tvGenresCat: Array
    },

    watch: {
        movieSearch: function() {
            this.movieSearch.forEach(movie => {
                this.id = [];
                this.id.push(movie.id)
            })
        }
    }
}
</script>

<style lang="scss" scoped>
@import '../assets/style/common.scss';
@import '../assets/style/variables.scss';

    .catalogue {
        background-color: $primary-color;
        height: calc(100vh - $header-height);
        overflow-y: auto;
    }

    ul {
        display: flex;
        flex-wrap: wrap;
        width: 100%;
    }

    li{
        list-style: none;
        margin: 1rem;
        width: calc(25% - 2rem);
    }

</style>