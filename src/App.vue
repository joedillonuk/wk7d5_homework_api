<template>
  <div id="app">
<h1>Choose a Pokemon (this is App)</h1>
<!-- <p v-for="(pokemon, index) in this.allPokemon" :value="pokemon" :key="index">{{pokemon.name}}</p> -->
<pokemon-choose :allPokemon="allPokemon"></pokemon-choose>
<pokemon-detail :selectedPokemon="selectedPokemon"></pokemon-detail>
  </div>
</template>

<script>
import { eventBus } from "@/main.js";

import PokemonChoose from './components/PokemonChoose.vue';
import PokemonDetail from './components/PokemonDetail.vue';


export default {
  name: 'App',
  data(){
    return {
      allPokemon: null,
      selectedPokemon: null,
    }
  },
  components: {
    "pokemon-choose": PokemonChoose,
    "pokemon-detail": PokemonDetail,

  },
  methods: {

    fetchPokemonObject: function(selectedPokemon) {
      console.log(selectedPokemon.url);

      return fetch(`${selectedPokemon.url}`)
      .then(res => res.json())
      .then(selectedPokemon => this.selectedPokemon = selectedPokemon)
      // console.log(result);
    }


  },
  mounted(){
    fetch('https://pokeapi.co/api/v2/pokemon?limit=970')
    .then(res => res.json())
    .then(allPokemon => this.allPokemon = allPokemon.results)

eventBus.$on("pokemon-choose", selectedPokemon => (this.fetchPokemonObject(selectedPokemon)));


}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
