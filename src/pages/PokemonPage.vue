<template>
    <div class="logo">
        <img src="@/assets/pokemon_logo.png" alt="">
    </div>
    <h1 v-if="!pokemon">Espere porfavor...</h1>
    <div v-else>
        
        <div class="container-grid">
            <div class="img-poke">
                <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon" />
                <div class="quiz">
                    <h1>¿Quien es este pokemon?</h1>
                    <PokemonOptions
                    :pokemons="pokemonArr"
                    :election="election"
                    @selection="checkAnswer($event)" />

                    <template v-if="showAnswer">
                        <h2 class="fade-in">{{ message }}</h2>
                        <button @click="newGame">Nuevo juego</button>
                    </template>
                </div>
                <div v-if="showPokemon" class="data">
                    <h2>Poke info</h2>
                    <PokemonData 
                    :name="this.pokemon.name"
                    :types="pokemonTypes"
                    :abilities="abilitiesArr" />
                </div>
            </div>

        </div>

    </div>
</template>

<script>
import PokemonPicture from "@/components/PokemonPicture.vue";
import PokemonOptions from "@/components/PokemonOptions.vue";
import PokemonData from "@/components/PokemonData.vue"

import {getPokemonOptions, getPokemonData} from "@/helpers/getPokemonOptions";
// import getPokemonTypes from "@/helpers/getPokemonOptions";

export default {
  components: {
    PokemonPicture,
    PokemonOptions,
    PokemonData
  },
  data() {
    return {
      pokemonArr: [],
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      election: false,
      pokemonTypes: [],
      abilitiesArr: [],
      message: ''
    };
  },
  methods: {
    async mixPokemonArray() {
      this.pokemonArr = await getPokemonOptions();

      const rndInt = Math.floor(Math.random() * 4);
      this.pokemon = this.pokemonArr[rndInt];

      

    },
    checkAnswer(pokemonId) {
        this.showPokemon = true
        this.showAnswer = true
        this.election = true
        if(pokemonId == this.pokemon.id) {
            this.message = `Correcto, ${this.pokemon.name}`
            this.getTipos(this.pokemon.id)
            this.getAbilities(this.pokemon.id)
        } else {
            this.message = `Fallaste, era ${this.pokemon.name}`
            this.getTipos(this.pokemon.id)
            this.getAbilities(this.pokemon.id)
        }

    },
    newGame() {
        this.showPokemon = false
        this.showAnswer  = false
        this.pokemonArr  = []
        this.pokemonTypes = []
        this.abilitiesArr = []
        this.pokemon     = null
        this.election    = false
        this.mixPokemonArray()
    },
    async getTipos(pokeId) {
        const res = await getPokemonData(pokeId);
        this.pokemonTypes = res.data.types
    },
    async getAbilities(pokeId) {
        const res = await getPokemonData(pokeId);
        this.abilitiesArr = res.data.abilities
    }
  },
  mounted() {
    this.mixPokemonArray();
    
  },
};
</script>

<style scoped>

    .logo img {
        width: 300px;
    }

    .container-grid {
        display: grid;
        grid-template-columns: repeat(1,1fr);
        width: 60%;
        margin: 0 auto;
        background-color: #CE1131;
        padding: 10px;
        border-radius: 10px;
    }

    .img-poke {
        /* border-right: 5px solid white; */
    }

    .quiz {
        background-color: khaki;
        border-radius: 15px;
        width: 80%;
        margin: 0 auto;
        padding: 10px;
    }
    .quiz h2 {
        text-transform: capitalize;
    }

    button {
        background-color: #FFB200;
        border: none;
        padding: 10px;
        border-radius: 10px;
        cursor: pointer;
    }

    @media(max-width: 700px) {
        .container-grid {
            width: 90%;
        }

        .quiz {
            width: 90%;
        }

        
    }

</style> 