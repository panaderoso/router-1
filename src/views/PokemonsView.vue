<script setup>
//import axios from "axios";
//import { ref } from "vue";
import { RouterLink } from "vue-router";
import { useGetData } from "@/composables/getData";

//const pokemons = ref([]);

const { data, getData, loading, error } = useGetData();

/*const getData = async () => {
  try {
    const { data } = await axios.get("https://pokeapi.co/api/v2/pokemon");

    //console.log(data.results.name);
    pokemons.value = data.results;
  } catch (error) {
    console.log(error);
  }
};*/

getData("https://pokeapi.co/api/v2/pokemon");
</script>
<template>
  <h1>Pokemons</h1>
  <p v-if="loading">Cargando Información...</p>
  <div class="alert alert-danger mt-2" v-if="error">{{ error }}</div>
  <div v-else>
    <ul class="list-group">
      <!--<li v-for="poke in pokemons">-->
      <li class="list-group-item" v-for="poke in data.results">
        <RouterLink :to="`/pokemons/${poke.name}`">{{ poke.name }}</RouterLink>
      </li>
    </ul>
    <div class="mt-2">
      <button
        :disabled="!data.previous"
        class="btn btn-success me-2"
        @click="getData(data.previous)"
      >
        Previous
      </button>
      <button
        :disabled="!data.next"
        class="btn btn-primary"
        @click="getData(data.next)"
      >
        Next
      </button>
    </div>
  </div>
</template>
