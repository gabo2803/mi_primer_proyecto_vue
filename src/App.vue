<script setup>

import { ref , computed } from 'vue';

const name = "Vue dinamico";

const counter = ref(0)
const arrayfavoritos = ref([])
//incrementar, decrementar y resetear con los botones
const increment = () => counter.value++;
const decrement = () =>counter.value--;
const reset = () => (counter.value = 0);

const add = () =>{
  arrayfavoritos.value.push(counter.value)
};
// Bloquear boton add
const bloquearBtnAdd = computed(()=>{
  const numSearch = arrayfavoritos.value.find((num)=> num === counter.value);
  return numSearch || numSearch === 0;
});
//Cambiar de color el counter
const classcounter = computed(()=>{
  if(counter.value > 0){
    return  "positivo";
  }
  if(counter.value < 0){
    return "negativo";
  }
  if(counter.value){
    return "zero";
  }
});
</script>

<template>
  <div class="container text-center mt-3">
    <h1>Hola {{ name.toUpperCase()}}</h1>
  <h2 :class="classcounter">{{ counter }}</h2>
  <div class="btn-group">
    <button @click="increment" class="btn btn-success">Aumentar</button>
    <button @click="decrement" class="btn btn-danger">Disminuir</button>
    <button @click="reset" class="btn btn-secondary">Reset</button>
    <button @click="add" :disabled="bloquearBtnAdd" class="btn btn-primary">Add</button>
  </div>
  <ul class="list-group mt-3">
    <li v-for="(num, index) in arrayfavoritos" :key="index" class="list-group-item">
      {{ num }}</li>
  </ul>
  </div> 

</template>


<style>
 h1{
  color: red;
 }
 .positivo{
  color: green;
 }
 .negativo{
  color: red;
 }
 .zero{
  color:black
 }


</style>