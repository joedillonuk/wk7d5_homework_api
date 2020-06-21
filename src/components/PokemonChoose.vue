<template lang="html">

  <div>
    <h2>Choose a Pokemon!</h2>
  <form v-on:submit.prevent>
    <input type="text" v-model="search" placeholder="search Pokemon..." v-on:keyup="searchPokemon">
    <select v-on:change="handleSelect" v-model="selectedPokemon">
      <option disabled value="">Select a Pokemon...</option>
      <option v-for="(pokemon, index) in allPokemon" :value="pokemon" :key="index">{{pokemon.name}}</option>
    </select>
  </form>
  <pokemon-list :searchList="searchList"></pokemon-list>
</div>
</template>

<script>
import { eventBus } from '../main.js'
import PokemonList from '../components/PokemonList.vue';


export default {
  name: "pokemon-choose",
  data(){
    return {
      "search": "",
      "searchList": "",
      "selectedPokemon": {},
    }
  },
  components: {
    "pokemon-list": PokemonList,
  },
  props: ["allPokemon"],
  methods: {
    searchPokemon(){
      let foundPokemon = this.allPokemon.filter((pokemon) => {
        return pokemon.name.toLowerCase().includes(this.search.toLowerCase())
      })
      this.searchList = foundPokemon
      eventBus.$emit('pokemon-search', this.searchList)
    },
    handleSelect(){
      this.search = ""
      this.searchList = null
      eventBus.$emit('pokemon-choose', this.selectedPokemon)
    },
    clickedPokemon(pokemon){
    this.selectedPokemon = pokemon
    this.handleSelect();
    }
  },
  mounted(){
    eventBus.$on("pokemon-list", selectedPokemon => this.clickedPokemon(selectedPokemon));
  }
}
</script>

<style lang="css" scoped>
form{
  text-align: center;
  margin: 40px 0;
  background-color: lightblue;

}

select, input[type="text"]{
  font-size: 18px;
  background-color: white;

}

select {
  margin-left: 20px;
  background-color: white;

}
</style>
