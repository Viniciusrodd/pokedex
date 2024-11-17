

<template>
  <div id="pokemon">
    <div class="card">
        <div class="card-image">
            <figure>
            <img
                :src="pokemon.frontPoke"
                alt="Placeholder image"
            />
            </figure>
        </div>

      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{ num }}. {{ upper(nome) }}</p>
            <p class="subtitle is-6">{{ pokemon.typePoke }}</p>
          </div>
        </div>

        <div class="content">
            
        </div>
      </div>
    </div>
  </div>
</template>



<script>
import axios from 'axios';

export default {
    created(){
      axios.get(this.url)
        .then((res) =>{
          //Criando var type pra receber tipo de pokemon:
          this.pokemon.typePoke = res.data.types[0].type.name;
          //Pegando imagem de pokemon, frente/costas:
          this.pokemon.frontPoke = res.data.sprites.front_default;          
          this.pokemon.backPoke = res.data.sprites.back_default;
          console.log(this.pokemon)
        })
    },

    data(){
      return { 
        pokemon: {
          typePoke: '',   // Inicializando com uma propriedade vazia
          frontPoke: '',  // Inicializando com uma propriedade vazia
          backPoke: ''
        }
      }
    },

    props: {
      num: Number,
      nome: String,
      url: String
    },

    methods: {
      //transforma 1 letra de string em maiúscula:
      upper(value){
        if(!value){
          return ''
        }else{          
          return value[0].toUpperCase() + value.slice(1)
        }
      }
    }
}
</script>



<style>
    #pokemon{
        margin: 40px 0px 40px 0px;
    }
</style>