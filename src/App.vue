<template>
  <div id="app">
<img src="../public/pokemon_logo.png" alt="Pokemon Logo">
<!-- <p v-for="(pokemon, index) in this.allPokemon" :value="pokemon" :key="index">{{pokemon.name}}</p> -->
<pokemon-choose :allPokemon="allPokemon"></pokemon-choose>
<pokemon-detail :selectedPokemon="selectedPokemon"></pokemon-detail>
<br>

<canvas  id="canvas" width="150" height="150"></canvas>
  </div>

</template>

<script>
import { eventBus } from "@/main.js";

import PokemonChoose from './components/PokemonChoose.vue';
import PokemonDetail from './components/PokemonDetail.vue';

function draw() {
  var canvas = document.getElementById('canvas');
  if (canvas.getContext) {
    var ctx = canvas.getContext('2d');

    ctx.beginPath();

      ctx.arc(75, 75, 75, 0, Math.PI * 1, true); // Pokeball outline
      ctx.fillStyle = "red";
      ctx.fill();
      ctx.arc(75, 75, 75, 0, Math.PI * 2, true); // Pokeball outline

      ctx.moveTo(150, 75);
      ctx.arc(75, 75, 30, 0, Math.PI * 2, false);  // pokeball middle outer
      ctx.fillStyle = "white";
      ctx.fill('evenodd');
      ctx.moveTo(90, 75);
      ctx.arc(75, 75, 15, 0, Math.PI * 2, false);  // Pokeball middle inner
      ctx.fillStyle = "white";
      ctx.fill('evenodd');
      ctx.moveTo(45, 75);
      ctx.lineTo(0, 75);
      ctx.fillStyle = "red";
      // ctx.fill('');
      // ctx.stroke();

  }
}

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
// eventBus.$on("pokemon-list", selectedPokemon => (this.fetchPokemonObject(selectedPokemon)));
draw();

}
}
</script>

<style>

* {
  background-color: lightblue;

}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
canvas {  }

</style>
