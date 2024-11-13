<template>
  <div id="app">
    <h1>Meu projeto vue</h1>
    <ul>
      <li v-for="(pokemon, index) in pokemonVar" :key="pokemon.id">
        {{ index + 1 }} - {{ pokemon.name }}
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'App',
  data() {
    return {
      pokemonVar: []
    }
  },
  created(){
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0')
      .then(response =>{      
        console.log(`Pegou a lista de pokemons ${this.pokemonVar}`)
        this.pokemonVar = response.data.results; 
      })
      .catch(error => console.log(error))
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
