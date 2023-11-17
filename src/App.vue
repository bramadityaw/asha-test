<script setup>
import { ref } from 'vue'
import PokemonEntries from './components/PokemonEntries.vue'

const title = ref('PokeDex Web')
</script>

<template>
  <div class="bg-dark" style="padding: 1rem 1rem; border-radius: 25px;">
    <h1>{{ title }}</h1>
    <PokemonEntries></PokemonEntries>
  </div>
</template>

<style scoped>

</style>
