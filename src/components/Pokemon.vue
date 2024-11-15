

<template>
  <div>
    <h1>{{ num }} {{ upper(nome) }}</h1>
    <small>{{ url }}</small>
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

</style>