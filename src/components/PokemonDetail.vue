<template lang="html">
  <div>

    <div>
      <div v-if="selectedPokemon" id="pokemonDetail">
        <div id="detailWrapper">
          <h2>{{selectedPokemon.name}}</h2>
          <div id="flexWrapper">
            <div id="left">
              <!-- <p><span>Name: {{selectedPokemon.name}}</span></p> -->
              <p><b>Type: </b>{{selectedPokemon.types[0].type.name}}</p>
              <p><b>Height: </b>{{selectedPokemon.height}}</p>
              <p><b>Weight: </b>{{selectedPokemon.weight}}</p>
<h3>Abilities</h3>
<ul>
  <li>{{selectedPokemon.abilities[0].ability.name}}</li>
  <li>{{selectedPokemon.abilities[1].ability.name}}</li>

</ul>
              <!-- <button v-on:click="handleFave" type="button" name="button">Add to favourites</button> -->
            </div>
            <div id="right">
              <img :src="selectedPokemon.sprites.front_default" alt="Pokemon">
            </div>
          </div>
        </div>
      </div>

      <!-- <div v-if="favourites" id="pokemonDetail">
      <div id="detailWrapper" v-for="(pokemon, index) in favourites" :value="pokemon" :key="index">
      <h2>{{pokemon.name}}</h2>
      <div id="flexWrapper">
      <div id="left">
      <p><span>Name: {{pokemon.name}}</span></p>
      <p>URL placeholder: {{pokemon.url}}</p>
      <button v-on:click="handleFave" type="button" name="button">Add to favourites</button>
    </div>
    <div id="right">
    <img :src="https://www.serebii.net/pokemonmasters/pokemon/025.png" alt="Pokemon">
  </div>
</div>
</div>
</div> -->

</div>
</div>
</template>

<script>
// import { eventBus } from '../main.js'


export default {
  name: 'pokemon-detail',
  data(){
    return{
    }
  },
  computed: {


  },
  props: ["selectedPokemon"],
  methods: {
    handleFave(){
      // this.favourites.push(this.beer)
      // eventBus.$emit('beer-fave', this.favourites)
      console.log("fave clicked");

    }
  },
  mounted(){

  },

}
</script>

<style lang="css" scoped>
#pokemonDetail {
  box-sizing: border-box;
  height: 100%;
  width: 500px;
  background: #3c5aa6;
  color: #222;
  padding: 5px;
  margin-left: 10px;
  border: 1px solid #ccc;
  margin: 0 auto;
  text-align: left;
  border-radius: 10px;

}

#detailWrapper {
  box-sizing: border-box;
  background: #fff;
  padding: 30px;
  height: 100%;
  border-radius: 20px;
  background-color: lightblue;

}

#flexWrapper {
  display: flex;
  justify-content: space-between;
}

#left, #right {
  width: 45%;
}

#right img {
  display: block;
  margin-left: auto;
  margin-right: auto;
  height: 200px;
  width: auto;
}

#left p:first-child {
  margin-top: 0;
}

h2 {
  margin: 10px 0 20px;
  padding: 0;
}

p span {
  font-weight: bold;
}

ul {
   list-style-type: none;
}



</style>
