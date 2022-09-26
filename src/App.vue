<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
    <img src="./assets/logoC.jpg" alt="coffeeBreak">
    <hr>
    <h4 class="is-size-4">Pokedex</h4>
    <input class="input is-rounded" type="text"
           placeholder="Search pokemon by name"
           v-model="searchPokemon"
    >
    <button class="button is-fullwidth is-success"
            id="searchBtn"
            @click="searching"
    >Search</button>
      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
        <comp-pokemon :name="poke.name" :url="poke.url" :num="index + 1" />
      </div>
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
      pokemons: [],
      filteredPokemons: [],
      searchPokemon: '',
    }
  },
  created: function() {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&0ffset=0")
         .then(res => {
          console.log('Got the pokemon list');
          this.pokemons = res.data.results;
          this.filteredPokemons = res.data.results;
         })
  },
  methods: {
    searching: function() {
      this.filteredPokemons = this.pokemon;
      if (this.searchPokemon == '' || this.searchPokemon == ' ') {
         this.filteredPokemons = this.pokemons;
      } else {
         this.filteredPokemons = this.pokemons
             .filter(pokemon => pokemon.name == this.searchPokemon)
      }
    }
    },
  /*
  computed: {
    searchResult: function() {
      if (this.searchPokemon == '' || this.searchPokemon == ' ') {
        return this.pokemons;
      } else {
        return this.pokemons.filter(pokemon => pokemon.name == this.searchPokemon)
      }
    }
  }
  */
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

#searchBtn {
  margin-top: 2%;
}
</style>
