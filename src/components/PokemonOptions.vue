<template>
    <div class="options-container">
        <ul>
            <li
              v-for="pokemon in pokemons"
              :key="pokemon.id"
              @click="decision(pokemon.id)">
              {{ pokemon.name }}
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    props: {
        pokemons: {
            type: Array,
            required: true
        },
        election: {
            type: Boolean,
            required: true
        }
    },
    methods: {
        decision(pokemonId) {
            if(this.election) return
            this.$emit('selection', pokemonId)
        }
    }
}
</script>

<style scoped>
    ul {
        list-style-type: none;
    }
    li {
        background-color: white;
        border-radius: 5px;
        border: 1px solid rgba(0, 0, 0, 0.2);
        cursor: pointer;
        margin-bottom: 10px;
        width: 250px;
    }

    li:hover {
        background-color: rgba(0, 0, 0, 0.05);
    }

    .options-container {
        display: block;
    }

    .options-container ul {
        display: grid;
        grid-template-columns: repeat(2,1fr);
    }

    .options-container ul li {
        display: grid;
        width: 90%;
        text-transform: capitalize;
        padding: 10px;
    }

    @media(max-width: 700px) {
        .options-container {
            width: 90%;
            margin: 0 auto;
            text-align: center;
        }

        .options-container ul {
            width: 80%!important;
        }

        .options-container ul li {
            width: 80%;
        }
    }
</style>