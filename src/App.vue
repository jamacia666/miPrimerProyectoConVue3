<script setup>
import {ref,computed} from 'vue' 
const name="Vue dinámico"
const counter= ref(0)
const arrayFavoritos= ref([])
const increment = () => {
  console.log("aumentar contador");
  counter.value ++;
 
}
const decrement = () => {
  console.log("disminuir contador");
  counter.value --;
 
}

const add = () => {
  arrayFavoritos.value.push(counter.value); 
}

const bloquearBtnAdd= computed(()=> {
  const numSearch = arrayFavoritos.value.find(num => num=== counter.value)
  console.log(numSearch)
  return numSearch || numSearch===0
})
const reset = () => {
  console.log("resetear contador");
  counter.value =0
 
}
const classCounter = computed(() => {
  if (counter.value== 0) {
    return  'zero'
  }
  if (counter.value> 0) {
    return  'positive'
  }
  if (counter.value < 0) {
    return  'negative' 
 }

})



</script>
<template>
  <div class="container text-center mt-3">
    <h1> Hola  {{name.toUpperCase()}}</h1>
  <br/>
  <h2 :class="classCounter">{{counter}}</h2>
  <div class="btn-group">
    <button @click="increment" class="btn btn-success">Increment</button>
    <button @click="decrement" class="btn btn-danger">Decrement</button>
    <button @click="reset" class="btn btn-secondary">Reset</button>
   <button @click="add" :disabled="bloquearBtnAdd" class="btn btn-primary">Add</button>
  </div>
  <ul class="list-group mt-4">
     <li class="list-group-item"
       v-for="(num,index) in arrayFavoritos"
       :key="index"
     >
        {{num}}
     </li>

  </ul>
  </div>
 

</template>
<style>
h1 {
  color:red;
}

.negative {
  color: red;
}

.positive {
  color: green;
}
.zero {
  color: peru;
}

</style>
