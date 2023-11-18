<script setup>
import { ref } from 'vue'

const filterTextForName = ref('')
const pokemonTypesList = ref([
  'normal',
  'fighting',
  'flying',
  'poison',
  'ground',
  'rock',
  'bug',
  'ghost',
  'steel',
  'fire',
  'water',
  'grass',
  'electric',
  'psychic',
  'ice',
  'dragon',
  'dark',
  'fairy',
  'unknown',
  'shadow'
])
</script>
<template>
  <div style="position: sticky; padding-top: 1.25rem; top: 0">
    <div class="card bg_white">
      <p>{{ filterTextForName }}</p>
      <label for="searchPokemonByName">Search Pokemon by Name</label>
      <input type="text" v-model="filterTextForName" id="searchPokemonByName" />
      <label for="searchPokemonByTypes">Select up to 2 types</label>
      <select name="types" id="searchPokemonByTypes">
        <option v-for="type in pokemonTypesList" :value="type" :key="type"> {{ type[0].toUpperCase() + type.slice(1)}} </option>
      </select>
    </div>
  </div>
</template>
<style scoped>
input,
select {
  display: block;
}
</style>
