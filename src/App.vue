<template>
  <div id="app">
    <div v-for="(poke, index) in pokemons" :key="index">
      <comp-pokemon :name="poke.name" :url="poke.url" :num="index + 1" />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import CompPokemon from './components/CompPokemon.vue';

export default {
  name: 'App',
  components: {
    CompPokemon
  },
  data() {
    return {
      pokemons: []
    }
  },
  created: function() {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&0ffset=0")
         .then(res => {
          console.log('Got the pokemon list');
          this.pokemons = res.data.results;
         })
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
