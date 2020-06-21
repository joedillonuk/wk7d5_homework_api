<template lang="html">

  <div>
    <ul>
      <li class="btn success" v-on:click="handleSelect(pokemon)" v-for="(pokemon, index) in searchList" :value="pokemon" :key="index">{{pokemon.name}}</li>
      </ul>
    </div>
  </template>

  <script>
  import { eventBus } from '../main.js'

  export default {
    name: "pokemon-list",
    data(){
      return {
        "search": "",
        "selectedPokemon": {},
      }
    },
    props: ["searchList"],
    methods: {

      handleSelect(pokemon){
        this.search = ""
        this.selectedPokemon = pokemon
        eventBus.$emit('pokemon-list', this.selectedPokemon)

      }
    }
  }
  </script>

  <style lang="css" scoped>
  .btn {
    border: none;
    background-color: inherit;
    padding: 14px 28px;
    font-size: 16px;
    cursor: pointer;
    display: inline-block;
  }

  .btn:hover {background: #eee;}

  .success {color: black;}

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
