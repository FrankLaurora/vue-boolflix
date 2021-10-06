<template>
    <div>
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
    li{
        list-style: none;
        margin-block: 1rem;
    }

</style>