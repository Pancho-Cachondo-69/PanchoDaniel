<script setup>
import {ref,computed} from 'vue'

const name = 'Vue dinamico';
const styleColor = "color: blue";
const arrayColores =["azul","red","peru"];
const activo = true;
const arrayFrutas = [
        {
            name: "Manzana",
            price: "$1.00",
            description: "Una manzana",
            stock:20
        },
        {
            name: "Pera",
            price: "$2.00",
            description: "Una pera",
            stock:20
        },
        {
            name: "Naranja",
            price: "$3.00",
            description: "Una naranja",
            stock:20
        },
    ];
    const objetoFrutas = {
            name: "Manzana",
            price: "$1.00",
            description: "Una manzana",
            id:1,
            stock:20
        };

const handClick = (messager)=>{
  console.log(messager);
}

let aumentar = ref(0);
const increment =()=> aumentar.value ++;
const resetea = ()=> (aumentar.value = 0);
const decrementar = ()=> aumentar.value --;
const classComputer = computed (()=>{
  if(aumentar.value === 0)
    return 'zero'
  if(aumentar.value>0)
    return 'positive'
  if(aumentar.value<0)
    return 'negativo'
});
const arrayList = ref([]);
const add = ()=>{
  arrayList.value.push(aumentar.value)
}
const bloquAdd = computed(()=>{
  const numSerach = arrayList.value.find(num =>num ===aumentar.value);
  console.log(numSerach);
  //if(numSerach === 0) return true;
  //return numSerach ? true : false;
  return numSerach || numSerach ===0 ;
});
</script>

<template>
  <h1>{{name.toUpperCase()}}</h1>
  <h2>{{ arrayColores }}</h2>
  <h2 :style="`color: ${arrayColores[2]}`">Soy azul</h2>
  <h2>{{ activo ? "Estoy activo" : "Estoy inactivo" }}</h2>
  <p v-if="activo == true">
    <span>Icono</span>
    Estoy activo</p>
  <p v-else-if="activo ==false">Estoy inactivo</p>
  <p v-else>Estoy indeciso</p>
  <h2 v-show="activo">Estoy inactivo v-show</h2>
  <ul>
    <li v-for="(fruta, index) in arrayColores" :key="index">
      {{ index }} - {{ fruta }}
    </li>
  </ul>
  <ul>
    <li v-for="pancho in arrayFrutas" :key="pancho.id">
        {{ pancho.name }} - {{ pancho.price }} - {{ pancho.description }}
    </li>
  </ul>
  <ul>
    <li v-for="(value, propiedad, index) in objetoFrutas" :key="value">
       {{ index }} - {{ propiedad }} - {{ value }}
    </li>
  </ul>
  <ul>
    <template v-for="item in arrayFrutas" :key="item.name">
      <li  v-if="item.stock <0">
        {{item.name}} - {{item.price}}
      </li>
    </template>
    <!--li  v-for="item in arrayFrutas" :key="item.name" >
      <span v-if="item.stock <0">
        {{item.name}} - {{item.price}}
      </span>
    </li>-->
  </ul>
<button v-on:click.right="handClick('texto 1')">Activame 1</button>
<button @click.middle="handClick('texto 2')">Activame 2</button>
<h2 :class="classComputer">{{ aumentar }}</h2>
<button @click="increment" class="btn btn-success">aumentar</button>
<button @click="resetea" >reset</button>
<button @click="decrementar">decrementar</button>
<button @click="add" :disabled="bloquAdd">ADD</button><br>
{{ arrayList }}
<ul>
  <li v-for="(num, index) in arrayList" :key="index">
      {{ num }}
  </li>
</ul>
</template>

<style>
h1 {
color:red;
}
.positive{
  color:green;
}
.negativo{
  color:red;
}
.zero{
  color: peru;
}
</style>