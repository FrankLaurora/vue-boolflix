<template>
    <header>
        <h1>boolflix</h1>
        <div class="search_bar">
            <input type="text" v-model="titleSearch" @keyup.enter.prevent="$emit('searchByTitle', titleSearch)" placeholder="Cosa vuoi guardare?">
            <button @click.prevent="$emit('searchByTitle', titleSearch)">Cerca</button>
        </div>
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
@import '../assets/style/variables.scss';
    header {
        position: fixed;
        top: 0;
        display: flex;
        justify-content: space-between;
        align-items: center;
        background: linear-gradient(90deg, rgba(9,12,39,1) 0%, rgba(48,199,223,1) 100%);;
        height: $header-height;
        width: 100%;
        padding-inline: 1.5rem;
        box-shadow: 0px 0px 8px rgb(240, 253, 255) inset;

        h1, button {
            text-transform: uppercase;
            color:rgb(240, 253, 255);
            text-shadow: 0px 0px 8px rgb(48, 199, 223);
        }

        .search_bar {
            input, button {
                border: 2px solid $secondary-color;
                border-radius: 5px;
                outline: none;
            }

            input {
                padding: 0.5rem 1.5rem 0.5rem 0.5rem;
                margin-right: 1rem;
            }

            button {
                padding: 0.5rem 1rem;
                background-color: $secondary-color;
                font-weight: bold;
            }
        }
    }
 
</style>