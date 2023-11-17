<script setup>
import { ref } from 'vue'
import PokemonEntries from './components/PokemonEntries.vue'

const title = ref('PokeDex Web')
</script>

<template>
  <div class="bg-dark app-container">
    <div class="title">
      <img src="/src/assets/pokeball.webp" alt="" class="inline_img">
      <h1>{{ title }}</h1>
      <img src="/src/assets/pokeball.webp" alt="" class="inline_img">
    </div>
    <PokemonEntries></PokemonEntries>
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
