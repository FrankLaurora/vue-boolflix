<template>
    <div>
        <div v-if="series == undefined">
            <h2>{{movie.title}}</h2>
            <h3>{{movie.original_title}}</h3>
            <img :src="`https://www.unknown.nu/flags/images/${movie.original_language}-100`" :alt="movie.original_language">
            <h3>{{roundedScore(movie.vote_average)}}</h3>
            <img :src="(movie.poster_path != null) ? `https://image.tmdb.org/t/p/w185/${movie.poster_path}` : 'https://via.placeholder.com/185x278/CECECE/000000/?text=Image+not+found.com'" alt="">
        </div>
        <div v-else>
            <h2>{{series.name}}</h2>
            <h3>{{series.original_name}}</h3>
            <img :src="`https://www.unknown.nu/flags/images/${series.original_language}-100`" :alt="series.original_language">
            <h3>{{roundedScore(series.vote_average)}}</h3>
            <img :src="(series.poster_path != null) ? `https://image.tmdb.org/t/p/w185/${series.poster_path}` : 'https://via.placeholder.com/185x278/CECECE/000000/?text=Image+not+found.com'" alt="">
        </div>
    </div>
</template>

<script>
export default {
    name: 'Card',

    props: {
        movie: Object,
        series: Object
    },

    methods: {
        roundedScore: function(num) {
            let roundedNum = Math.ceil(num / 2);

            return roundedNum
        }
    }
}
</script>

<style lang="scss" scoped>

</style>