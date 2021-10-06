<template>
    <div class="catalogue">
        <div class="container">
            <ul>
                <li v-for="element in movieSearch" :key="element.id">
                    <Card :movie="element"/>
                </li>
            </ul>
            <ul>
                <li v-for="element in seriesSearch" :key="element.id">
                    <Card :series="element"/>
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

    props: {
        movieSearch: Array,
        seriesSearch: Array
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
    }

    li{
        list-style: none;
        margin: 1rem;
        width: calc(25% - 2rem);
        text-align: center;
    }

</style>