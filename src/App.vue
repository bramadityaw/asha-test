<script setup>
import { onMounted, ref } from 'vue'

const hello = ref('Hello!')
const pokemonList = ref([])

onMounted(async () => {
  const pokemonData = await (fetch('https://pokeapi.co/api/v2/pokedex/1'))
  .then(response => response.json())
  
  pokemonList.value = pokemonData.pokemon_entries
})
</script>

<template>
  <div class="bg-dark" style="padding: 1rem 1rem; border-radius: 25px;">
    <h1>{{ hello }}</h1>
    <p>{{pokemonList[0]}}</p>
    <ul>
      <li v-for="pokemon in pokemonList" :key="pokemon.entry_number">
        ID: {{ pokemon.entry_number }}
        Pokemon Name: {{ pokemon.pokemon_species.name }}
      </li>
    </ul>
  </div>
</template>

<style scoped>

</style>
