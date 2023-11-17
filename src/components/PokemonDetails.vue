<script setup>
import { onMounted, reactive } from 'vue'

const props = defineProps({
  entry: Number
})

const pokemonDetails = reactive({ //Might add more detatls in the future
  types: Array
})

onMounted( async () => {
  const pokemonData = await fetch(`https://pokeapi.co/api/v2/pokemon/${props.entry}`)
  .then(response => response.json())

  pokemonDetails.types = pokemonData.types
})

</script>
<template>
  <div style="margin-bottom: 1.25rem; width: 100%;">
    <p>Type:</p>
    <ul>
      <li v-for="types in pokemonDetails.types" :key="types.slot">
        - {{ types.type.name[0].toUpperCase() + types.type.name.slice(1) }}
      </li>
    </ul>
  </div>
</template>
<style scoped>
  ul {
    margin: 0;
    padding: 0;
  }

  li {
    list-style-type: none;
  }
</style>