<template>

  <div class="container text-center mt-3">

    <h1> {{name.toUpperCase()}}</h1><br/>
    <h2 :class="classCounter"> {{counter}} </h2>

    <div class="btn-group">
      <button @click="increment" class="btn btn-success">aumentar</button>
      <button @click=" decrement" class="btn btn-danger">decrementar</button>
      <button @click="reset" class="btn btn-secondary">resetear</button>
      <button @click="add" :disabled="bloquearBtnAdd" class="btn btn-primary">Agregar</button>
    </div>
    <ul class="list-group mt-4">
      <li
      class="list-group-item"
      v-for="(num, index) in arrayFavorite" :key="index">{{num}}</li>
    </ul>


  </div>




</template>

<script setup>
  import {ref, computed} from 'vue';

  const name = ' hola Vue dinamico!';

  const counter = ref(0);

  const arrayFavorite = ref([])


  const increment = () =>{
    counter.value++;
  }
  const decrement = ()=>{
    counter.value--;
  }

  const reset = () => {
    counter.value = 0;
  }

  const add = ()=>{
    arrayFavorite.value.push(counter.value)
  }


  const bloquearBtnAdd = computed(()=>{
    const numSearch = arrayFavorite.value.find(num => num === counter.value)
    // if(numSearch === 0 )return true
    // return numSearch ? true : false;
    return numSearch || numSearch === 0;
  })

  const classCounter = computed(()=>{
    if(counter.value === 0){
      return 'zero';
    }
    if(counter.value > 0){
      return 'positive'
    }

    if(counter.value < 0){
      return 'negative'
    }
  })



</script>

<style>
  h1{
    color: aqua;
  }

  .positive{
    color: green;
  }
  .negative{
    color: red;
  }

  .zero{
    color: rgb(172, 111, 234);
  }
</style>
