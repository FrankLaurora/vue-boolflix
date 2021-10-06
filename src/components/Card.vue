<template>
    <div>
        <h2>{{movie.title}}</h2>
        <h3>{{movie.original_title}}</h3>
        <h3>{{movie.original_language}}</h3>
        <h3>{{movie.vote_average}}</h3>
    </div>
</template>

<script>
export default {
    name: 'Card',

    props: {
        movie: Object
    }
}
</script>

<style lang="scss" scoped>

</style>