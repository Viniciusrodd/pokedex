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
            
            <div id="div-btts">
                <button @click="buscar" id="search-btt" class="button is-primary is-dark">
                    Search
                </button>
                
                <button @click="reset" ref="bttResetRef" class="button is-danger is-dark" id="btt-reset">
                    Reset
                </button>
            </div>

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
            bttReset: true,
            filteredPokemons: [],
            pokemonVar: [],
            buscaName: '',
            pokeName: []
        };
    },

    methods: {
        bttDisplay(btt){
            if(btt){
                this.$refs.bttResetRef.style.display = 'block'
            }
        },
        buscar(){
            this.bttDisplay(this.bttReset)
            this.filteredPokemons = this.pokemonVar

            this.pokeName = this.filteredPokemons = this.pokemonVar.filter(pokemon => 
                    pokemon.name == this.buscaName
                )


            if(!this.buscaName == this.pokeName || this.buscaName == ''){
                window.alert(`esse pokemon "${this.buscaName}" não existe !`)
                this.filteredPokemons = this.pokemonVar
                this.buscaName = ''
            }
            else{
                console.log(this.buscaName + '=' + this.pokeName)
                this.pokeName
                this.buscaName = ''
            }
                        
        },
        reset(){
            this.filteredPokemons = this.pokemonVar
            this.buscaName = ''
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
#div-btts{
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: row;
}
#btt-reset{
    display: none;
    margin-top: 10px;
}
#search-btt{
    margin: 10px 5px 0px 0px;
}
#app {
     font-family: Avenir, Helvetica, Arial, sans-serif;
     -webkit-font-smoothing: antialiased;
     -moz-osx-font-smoothing: grayscale;
     text-align: center;
     margin-top: 60px;
}
</style>
