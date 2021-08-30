<template>
<div class="pokemon-container">
    <div class="card">
        <div class="content">
            <img
            v-if="!showPokemon"
            :src="imgSrc"
            class="hidden-pokemon"
            alt="pokemon">
            <img
            v-else
            :src="imgSrc"
            alt="pokemon">
        </div>
    </div>
    
</div>
    
</template>

<script>
export default {
    props: {
        pokemonId: {
            type: Number,
            required: true
        },
        showPokemon: {
            type: Boolean,
            required: true,
            default: false
        }
    },
    computed: {
        imgSrc() {
            return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.pokemonId}.svg`
        }
    }
}
</script>

<style scoped>
    
    /* Pokemon Picture */
    /* .pokemon-container {
        height: 200px;
    } */

    .pokemon-container {
        position: relative;
        display: flex;
        justify-content: center;
        align-items: center;
        max-width: 1200px;
        flex-wrap: wrap;
        z-index: 1;
    }

    .pokemon-container .card {
        position: relative;
        width: 280px;
        height: 400px;
        margin: 30px;
        /* box-shadow: 20px 20px 50px rgba(0, 0, 0, 0.5); */
        border-radius: 15px;
        background: rgba(105, 122, 127, 0.9);
        overflow: hidden;
        display: flex;
        justify-content: center;
        align-items: center;
        border-top: 1px solid rgba(255, 255, 255, 0.5);
        border-left: 1px solid rgba(255, 255, 255, 0.5);
        backdrop-filter: blur(5px);
    }

    /* .pokemon-container .card .content {
        padding: 20px;
        text-align: center;
        transform: translateY(100px);
        opacity: 0;
        transition: 0.5s;
    } */

    /* .pokemon-container .card:hover .content {
        transform: translateY(0px);
        opacity: 1;
    } */

    img {
        height: 200px;
        /* position: absolute; */
        /* right: 32%; */
        user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        -webkit-user-drag: none;
        -webkit-user-select: none;
    }
    .hidden-pokemon {
        filter: brightness(0);
    }
</style>