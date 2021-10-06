<template>
    <header>
        <input type="text" v-model="titleSearch" @keyup.enter.prevent="$emit('searchByTitle', titleSearch)">
        <button @click.prevent="$emit('searchByTitle', titleSearch)">Cerca</button>
    </header>
</template>

<script>
export default {
    name: 'Header',

    data() {
        return {
            titleSearch: ""
        }
    }
}
</script>

<style lang="scss" scoped>
 
</style>