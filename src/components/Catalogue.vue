<template>
    <div>
        <div v-for="(element, index) in userSearch" :key="index ">
            <Card :movie="element"/>
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
        userSearch: Array
    }
}
</script>

<style lang="scss" scoped>
    li{
        list-style: none;
        margin-block: 1rem;
    }

</style>