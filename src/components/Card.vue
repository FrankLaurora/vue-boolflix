<template>
    <div class="card">
        <div class="img_box" v-if="series == undefined">
            <img class="cover" :src="(movie.poster_path != null) ? `https://image.tmdb.org/t/p/w342/${movie.poster_path}` : `https://via.placeholder.com/185x278/CECECE/000000/?text=${movie.title}`" :alt="movie.title">

            <div class="info_box">
                <h2>{{movie.title}}</h2>
                <h3>{{movie.original_title}}</h3>
                <img :src="`https://www.unknown.nu/flags/images/${movie.original_language}-100`" :alt="movie.original_language">
                <div class="score">
                    <span v-for="(score, index) in 5" :key="index">
                        <i v-if="score <= roundedScore(movie.vote_average)" class="fas fa-star"></i>
                        <i v-else-if="score > roundedScore(movie.vote_average)" class="far fa-star"></i>
                    </span>
                </div>
            </div>
        </div>
        <div class="img_box" v-else>
            <!-- <h2>{{series.name}}</h2>
            <h3>{{series.original_name}}</h3> -->
            <!-- <img class="cover" :src="(series.poster_path != null) ? `https://image.tmdb.org/t/p/w342/${series.poster_path}` : `https://via.placeholder.com/185x278/CECECE/000000/?text=${series.name}`" :alt="series.name"> -->
            <!-- <img :src="`https://www.unknown.nu/flags/images/${series.original_language}-100`" :alt="series.original_language">
            <span v-for="(score, index) in 5" :key="index">
                <i v-if="score <= roundedScore(series.vote_average)" class="fas fa-star"></i>
                <i v-else-if="score > roundedScore(series.vote_average)" class="far fa-star"></i>
            </span> -->
            <img class="cover" :src="(series.poster_path != null) ? `https://image.tmdb.org/t/p/w342/${series.poster_path}` : `https://via.placeholder.com/185x278/CECECE/000000/?text=${series.name}`" :alt="series.name">

            <div class="info_box">
                <h2>{{series.name}}</h2>
                <h3>{{series.original_name}}</h3>
                <img :src="`https://www.unknown.nu/flags/images/${series.original_language}-100`" :alt="series.original_language">
                <div class="score">
                    <span v-for="(score, index) in 5" :key="index">
                        <i v-if="score <= roundedScore(series.vote_average)" class="fas fa-star"></i>
                        <i v-else-if="score > roundedScore(series.vote_average)" class="far fa-star"></i>
                    </span>
                </div>
            </div>
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
@import '../assets/style/common.scss';

    .card {
        position: relative;
        width: 100%;
        height: 400px;
        overflow: hidden;

        .img_box {
            height: 100%;
        }

        .cover {
            display: block;
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .info_box {
            display: none;
        }

        &:hover {

            .info_box {
                position: absolute;
                top: 0;
                right: 0;
                bottom: 0;
                left: 0;
                background-color: rgba(0, 0, 0, 80%);
                color: #fff;
                display: block;
            }
        }

    }

</style>