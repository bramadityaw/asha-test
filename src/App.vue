<script setup>
import { ref } from 'vue'
import PokemonEntries from './components/PokemonEntries.vue'
import FilterPokemon from './components/FilterPokemon.vue'

const title = ref('PokeDéx Web')
</script>

<template>
  <div class="bg_dark app-container">
    <div class="title">
      <img src="/src/assets/pokeball.webp" alt="" class="inline_img">
      <h1>{{ title }}</h1>
      <img src="/src/assets/pokeball.webp" alt="" class="inline_img">
    </div>
    <h3 style="text-align: center">Click and hold the 'Catch!' button to capture Pokémon!</h3>
    <div style="display: flex; justify-content: center;">
      <div style="position: relative; top: 0">
        <FilterPokemon/>
      </div>
      <PokemonEntries/>
    </div>
  </div>
</template>

<style scoped>
  .app-container {
    padding: 1rem 1rem;
    border-radius: 25px;
    min-width: 80dvh;
    margin: 1rem;
  }

  .title {
    margin: 0 auto 1.5rem;
    display: flex;
    justify-content: center;
  }

  .title h1 {
    width: fit-content;
    margin: 0 1rem;
  }
</style>
