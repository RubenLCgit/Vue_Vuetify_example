<script setup>

import { ref, computed } from 'vue';


  let countNoReactive = 0;

  let countReactive = ref(0);

  const numerosFavoritos = ref([]);

  let classColorNumber = computed(() => {
    if (countReactive.value > 0) {
      return 'positiveComputed';
    } else if (countReactive.value < 0) {
      return 'negativeComputed';
    } else {
      return 'neutralComputed';
    }
  });

  const incrementReactive = () => {
    countReactive.value++
  }

  const decrementReactive = () => {
    countReactive.value--
  }

  const reset = () => {
    countReactive.value = 0;
  }

let disponible = computed(() => {
  let count = 0;
  numerosFavoritos.value.forEach(element => {
    if (element === countReactive.value) {
      count++
    }
  });
  return count > 0 ? true : false;
});

const agregar = () => {
  numerosFavoritos.value.push(countReactive.value);
}

</script>

<template>

<v-card class="card"
  title="Colección de numeros favoritos"
  text="Busca y añade tus número favoritos"
  variant="tonal"
>
  <h3 :class="classColorNumber">{{ countReactive }}</h3>
  <v-card-actions>
    <v-btn block prepend-icon="$vuetify" variant="tonal" density="comfortable"  size="x-large" color="green" @click="incrementReactive">Aumentar</v-btn>
  </v-card-actions>
  <v-card-actions>
    <v-btn block prepend-icon="$vuetify" variant="tonal" density="comfortable" size="x-large" color="red" @click="decrementReactive">Disminuir</v-btn>
  </v-card-actions>
  <v-card-actions>
    <v-btn block prepend-icon="$vuetify" variant="tonal" density="comfortable" size="x-large" @click="reset">Resetear</v-btn>
  </v-card-actions>
  <v-card-actions>
    <v-btn block prepend-icon="$vuetify" variant="tonal" density="comfortable" size="x-large" color="blue" @click="agregar" :disabled="disponible">Agregar</v-btn>
  </v-card-actions>
</v-card>

<v-card class="card" text="Colección" variant="tonal">

  <ul>
    <li v-for="(numbers, index) in numerosFavoritos" :key="index">
      <v-card class="coleccion" variant="tonal">{{ numbers }}</v-card>
    </li>
  </ul>

</v-card>
  
</template>


<style scoped>

  h1 {
    color: rgba(255, 0, 225, 0.584);
  }

  .positiveComputed {
    color: green;
  }

  .negativeComputed {
    color: red;
  }

  .neutralComputed {
    color: white;
  }

  ul {
    list-style-type: none;
  }

  .card {
    margin: 10px;
    padding: 10px;
    border-radius: 10px;
    background-color: rgba(138, 74, 74, 0.5);
    text-align: center;
  }

  .v-btn{
    background-color: black;
  }

  .coleccion {
    margin: 10px;
    padding: 10px;
    border-radius: 10px;
    background-color: rgba(138, 74, 74, 0.5);
    text-align: center;
  }

</style>