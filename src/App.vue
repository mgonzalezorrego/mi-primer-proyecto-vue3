<script setup>
import { ref, computed } from "vue";

const nombre = "Vue dinamico";
const styleColor = "color: white";
const arrayColores = ["blue","red","peru"];
const activo = false;

const arrayFrutas = ["🍎", "🍌", "🍉", "🍓", "🍒"];

const arrayFrutasa = [
        {
            name: "Manzana",
            price: "$1.00",
            description: "Una manzana",
            stock: 0,
        },
        {
            name: "Pera",
            price: "$2.00",
            description: "Una pera",
            stock: 10,
        },
        {
            name: "Naranja",
            price: "$3.00",
            description: "Una naranja",
            stock: 20,
        },
    ];

  let counter = ref(0);
  const arrayFavoritos = ref([]);

  const handleClick = (mensaje) => {
    console.log(mensaje);
  }

  const incrementar = (operacion) => {
    if (operacion=="+") {
      counter.value++;
    } else if (operacion = "-") {
      counter.value--;
    }
    
  }

  const reset = () => {
    counter.value=0;
  }

  const add = () => {
    arrayFavoritos.value.push(counter.value)
  }

  const bloquearBtnAdd = computed(() => {
    const numSearch = arrayFavoritos.value.find((num) => num === counter.value)
    console.log(numSearch);
    if(numSearch === 0) return true
    return numSearch ? true : false;
    //return numSearch || numSearch === 0
  })

  const classCounter = computed(() => {
    if (counter.value === 0) {
      return 'zero'
    }
    if (counter.value > 0) {
      return 'positivo'
    }
    if (counter.value < 0){
      return 'negativo'
    }
  })
  

</script>

<template>
  <div class="container text-center mt-3">
    <h1>Hola {{nombre.toUpperCase()}}</h1>
    <h2 v-bind:style="styleColor">Soy Color Blanco</h2>
    <h2 :style="styleColor">Soy Color Blanco</h2>
    <h2>{{ arrayColores }}</h2>

    <h2 :style="`color: ${arrayColores[1]}`">Soy Rojo</h2>
    <h2>
      {{ activo ? "Estoy Activo" : "Estoy Inactivo"}}
    </h2>

    <h2 v-if="activo">
      <span>Icono</span> 
      Estoy Activo
    </h2>
    <p v-else>Estoy Inactivo 2</p>

    <h2 v-show="activo">Estoy Activo v-show</h2>
    <ul>
      <li v-for="(fruta, index) in arrayFrutas"
        :key="index">
      {{index}} - {{fruta}}      
      </li>
    </ul>

    <ul>
      <li v-for="item in arrayFrutasa" :key="item.name">
        {{item.name}} - {{item.price}} - {{item.description}}
      </li>
    </ul>

    <ul>
        <template v-for="item in arrayFrutasa" :key="item.name"> 
          <li v-if="item.stock > 0">{{ item.name }} - {{item.price}}</li>
        </template>
    </ul>


    <button v-on:click="handleClick('Activame 1')">Avisame 1</button>
    <button @click="handleClick('Activame 2')">Avisame 2</button>


    <h2 :class="classCounter">{{ counter }}</h2>
    <div class="btn-group">
      <button @click="incrementar('+')" class="btn btn-success">Aumentar</button>
      <button @click="incrementar('-')" class="btn btn-danger">Disminuir</button>
      <button @click="reset()" class="btn btn-secondary">Resetear</button>
      <button @click="add" :disabled="bloquearBtnAdd" class="btn btn-primary">Add</button>
    </div>
    <ul class="list-group">
      <li class="list-group-item" v-for="(num,index) in arrayFavoritos" :key="index">{{ num }}</li>
    </ul>
  </div>
</template>

<style>
h1 {
  color: red;
}
.positivo {
  color: green;
}
.negativo {
  color: red;
}
.zero {
  color: white;
}
</style>