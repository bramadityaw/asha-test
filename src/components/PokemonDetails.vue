<script setup>
import { onMounted, reactive, watch } from 'vue'

const props = defineProps({
  entry: Number,
  setTypes: Function
})

const pokemonDetails = reactive({
  types: Array
})

onMounted( async () => {
  const pokemonData = await fetch(`https://pokeapi.co/api/v2/pokemon/${props.entry}`)
  .then(response => response.json())

  pokemonDetails.types = pokemonData.types

  props.setTypes(props.entry, pokemonDetails.types)
})

watch(() => props.entry, async (newEntry) => {
  const pokemonData = await fetch(`https://pokeapi.co/api/v2/pokemon/${newEntry}`)
    .then(response => response.json())

  pokemonDetails.types = pokemonData.types

  props.setTypes(newEntry, pokemonDetails.types)
})

</script>
<template>
  <div style="margin-bottom: 1.25rem; width: 50%;">
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