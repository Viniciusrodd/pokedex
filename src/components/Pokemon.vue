

<template>
  <div>
    <h1>{{ num }} {{ upper(nome) }}</h1>
    <small>{{ url }}</small>
  </div>
</template>



<script>
export default {
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