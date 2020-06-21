<template lang="html">

  <div>
    <h2>Choose a Pokemon (this is PokemonChoose)</h2>
  <form v-on:submit.prevent>
    <input type="text" v-model="search" placeholder="search Pokemon..." v-on:keyup="searchPokemon">
    <select v-on:change="handleSelect" v-model="selectedPokemon">
      <option disabled value="">Select a Pokemon...</option>
      <option v-for="(pokemon, index) in allPokemon" :value="pokemon" :key="index">{{pokemon.name}}</option>
    </select>
  </form>
</div>
</template>

<script>
import { eventBus } from '../main.js'

export default {
  name: "pokemon-choose",
  data(){
    return {
      "search": "",
      "selectedPokemon": {},
    }
  },
  props: ["allPokemon"],
  methods: {
    searchPokemon(){
      let foundPokemon = this.allPokemon.filter((pokemon) => {
        return pokemon.name.toLowerCase().includes(this.search.toLowerCase())
      })
      this.selectedPokemon = foundPokemon

      eventBus.$emit('pokemon-choose', this.selectedPokemon)
    },
    handleSelect(){
      this.search = ""
      eventBus.$emit('pokemon-choose', this.selectedPokemon)
    }
  }
}
</script>

<style lang="css" scoped>
form{
  text-align: center;
  margin: 40px 0;
}

select, input[type="text"]{
  font-size: 18px;
}

select {
  margin-left: 20px;
}
</style>
