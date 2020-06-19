<template>
  <div id="app">

<p v-for="(pokemon, index) in this.AllPokemon" :value="pokemon" :key="index">{{pokemon.name}}</p>

  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return {
      AllPokemon: null
    }
  },
  components: {

  },
  mounted(){
    fetch('https://pokeapi.co/api/v2/pokemon?limit=100&offset=200')
    .then(res => res.json())
    .then(AllPokemon => this.AllPokemon = AllPokemon.results)
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
