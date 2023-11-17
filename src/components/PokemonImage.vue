<script setup>
import { ref, onMounted } from 'vue'

const props = defineProps({
  entry: Number
})

const pokemonImageURL = ref('')

onMounted( async () => {
  const pokemonData = await fetch(`https://pokeapi.co/api/v2/pokemon/${props.entry}`)
  .then(response => response.json())

  pokemonImageURL.value = pokemonData.sprites.front_default
})

pokemonImageURL.value = pokemonImageURL.value ? pokemonImageURL.value : '/src/assets/loader.svg'
</script>
<template>
  <img :src="pokemonImageURL" alt="">
</template>
<style scoped>
  
</style>