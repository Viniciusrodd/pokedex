<template>
     <div id="app">
        <div class="column is-half is-offset-one-quarter">
            <img class="image is-128x128" src="./assets/pokebola.png">
            <h1 class="title is-1">Welcome to my Pokedex</h1>
            <hr>
            <input placeholder="Search for a especific Pokemon name:" 
                v-model="buscaName" 
                type="text" 
                name="search" 
                class="input is-info">
            
            <button @click="buscar" id="search-btt" class="button is-primary is-dark">
                Search
            </button>

            <div v-for="(pokemon, index) in filteredPokemons" :key="pokemon.name">
                <Pokemon
                    :nome="pokemon.name"
                    :url="pokemon.url"
                    :num="index + 1"
                />
            </div>
        </div>
     </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon";

export default {
    components: {
        Pokemon
    },
    name: "App",

    data() {
        return {
            filteredPokemons: [],
            pokemonVar: [],
            buscaName: ''
        };
    },

    methods: {
        buscar(){
            this.filteredPokemons = this.pokemonVar
            if(this.buscaName == ''){
                this.filteredPokemons = this.pokemonVar
            }else{
                this.filteredPokemons = this.pokemonVar.filter(pokemon => 
                    pokemon.name == this.buscaName
                )
            }
        }
    },

    /*
    computed:{
        resultadoBusca(){
            if(this.buscaName == ''){
                return this.pokemonVar
            }else{
                return this.pokemonVar.filter(pokemon => 
                    pokemon.name == this.buscaName
                )
            }
        }
    },*/

    created() {
        axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
            .then((response) => {
                console.log(`Pegou a lista de pokemons ${this.pokemonVar}`);
                this.pokemonVar = response.data.results;
                this.filteredPokemons = response.data.results;
            })
            .catch((error) => console.log(error));
    },
};
</script>

<style>
#search-btt{
    margin-top: 10px;
}
#app {
     font-family: Avenir, Helvetica, Arial, sans-serif;
     -webkit-font-smoothing: antialiased;
     -moz-osx-font-smoothing: grayscale;
     text-align: center;
     margin-top: 60px;
}
</style>
