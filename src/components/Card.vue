<template>
    <div>
        <div v-if="series == undefined">
            <h2>{{movie.title}}</h2>
            <h3>{{movie.original_title}}</h3>
            <img :src="`https://www.unknown.nu/flags/images/${movie.original_language}-100`" :alt="movie.original_language">
            <span v-for="(score, index) in 5" :key="index">
                <i v-if="score <= roundedScore(movie.vote_average)" class="fas fa-star"></i>
                <i v-else-if="score > roundedScore(movie.vote_average)" class="far fa-star"></i>
            </span>
            <img :src="(movie.poster_path != null) ? `https://image.tmdb.org/t/p/w185/${movie.poster_path}` : 'https://via.placeholder.com/185x278/CECECE/000000/?text=Image+not+found.com'" alt="">
        </div>
        <div v-else>
            <h2>{{series.name}}</h2>
            <h3>{{series.original_name}}</h3>
            <img :src="`https://www.unknown.nu/flags/images/${series.original_language}-100`" :alt="series.original_language">
            <span v-for="(score, index) in 5" :key="index">
                <i v-if="score <= roundedScore(series.vote_average)" class="fas fa-star"></i>
                <i v-else-if="score > roundedScore(series.vote_average)" class="far fa-star"></i>
            </span>
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

    data() {
        return {
            scoreStars: []
        }
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
@import '../assets/style/common.scss'

</style>