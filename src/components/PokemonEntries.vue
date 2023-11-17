<script setup>
import { ref, onMounted } from 'vue'
import PokemonImage from './PokemonImage.vue'

const pokemonList = ref([])

onMounted(async () => {
  const pokedexData = await fetch('https://pokeapi.co/api/v2/pokedex/1')
  .then(response => response.json())
  
  pokemonList.value = pokedexData.pokemon_entries
})
</script>
<template>
  <div style="columns: 2;">
    <div v-for="pokemon in pokemonList" class="card bg-white" :key="pokemon.entry_number">
      <div class="card_image">
        <PokemonImage :entry="pokemon.entry_number"></PokemonImage>
      </div>
      <div class="card-info">
        <div class="card_title">
          <h1>{{ pokemon.pokemon_species.name }}</h1> <span class="pokemon_id">ID: {{ pokemon.entry_number }}</span>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
  .card {
    min-width: 240px;
    border-radius: 25px;
    border: 2px solid grey;
    padding: 1rem;
    margin: 0 .5rem .75rem;
    display: flex;
  }

  .card .card_image {
    width: 40%;
  }

  .card_image img {
    width: 100%
  }

  .card .card-info {
    width: 60%;
  }

  .card .card_title {
    display: flex;
    justify-content: space-between;
  }

  .card_title .pokemon_id {
    font-size: 1.75em;
  }

  .card h1 {
    font-size: 1.75em;
    border-bottom: 2px solid grey;
  }

  .card h2 {
    font-size: 1.5em;
  }

  .card h3 {
    font-size: 1.25em;
  }

  .bg-white {
    background-color: white;
    color: black;
  }
</style>