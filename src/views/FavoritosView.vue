<script setup>
import { useFavoritosStore } from "../store/favoritos";
import { storeToRefs } from "pinia";
import { RouterLink } from "vue-router";

const useFavoritos = useFavoritosStore();
const { favoritos } = storeToRefs(useFavoritos);
const { remove } = useFavoritos;
</script>

<template>
  <h1>Favoritos</h1>
  <p v-if="favoritos.length === 0">Sin favoritos</p>
  <ul v-else class="list-group">
    <li class="list-group-item" v-for="poke in favoritos" :key="poke.id">
      <div>
        {{ poke.name }}
      </div>
      <div>
        <router-link
          @click="remove(poke.id)"
          class="btn btn-sm btn-primary me-2"
          :to="`/pokemons/${poke.name}`"
        >
          Mas información
        </router-link>
        <button @click="remove(poke.id)" class="btn btn-sm btn-danger">
          Eliminar
        </button>
      </div>
    </li>
  </ul>
</template>
