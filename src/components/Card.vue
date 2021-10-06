<template>
    <div>
        <div v-if="series == undefined">
            <h2>{{movie.title}}</h2>
            <h3>{{movie.original_title}}</h3>
            <img :src="`https://www.unknown.nu/flags/images/${movie.original_language}-100`" :alt="movie.original_language">
            <h3>{{movie.vote_average}}</h3>
        </div>
        <div v-else>
            <h2>{{series.name}}</h2>
            <h3>{{series.original_name}}</h3>
            <img :src="`https://www.unknown.nu/flags/images/${series.original_language}-100`" :alt="series.original_language">
            <h3>{{series.vote_average}}</h3>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Card',

    props: {
        movie: Object,
        series: Object
    }
}
</script>

<style lang="scss" scoped>

</style>