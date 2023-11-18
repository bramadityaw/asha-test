<script setup>
import { ref, onMounted } from 'vue'
import PokemonImage from './PokemonImage.vue'
import PokemonDetails from './PokemonDetails.vue'
import PokemonStatus from './PokemonStatus.vue'

const pokemonList = ref([])

onMounted(async () => {
  const pokedexData = await fetch('https://pokeapi.co/api/v2/pokedex/1').then((response) =>
    response.json()
  )

  pokemonList.value = pokedexData.pokemon_entries.map((pokemon) => ({
    ...pokemon,
    isFavorite: false,
    dateFavorited: '',
    isCaptured: false,
    dateCaptured: '',
    dateReleased: ''
  }))
})

function toggleFavorite(pokemon) {
  pokemon.isFavorite = !pokemon.isFavorite
  if (pokemon.isFavorite) {
    const date = new Date()
    pokemon.dateFavorited = date.toLocaleDateString() + ' ' + date.toLocaleTimeString()
  }
}

function handlePokemonCapture(pokemon) {
  if (pokemon.isCaptured) {
    pokemon.isCaptured = false
    const date = new Date()
    pokemon.dateReleased = date.toLocaleDateString() + ' ' + date.toLocaleTimeString()
    return
  }
  pokemon.isCaptured = true
  const date = new Date()
  pokemon.dateCaptured = date.toLocaleDateString() + ' ' + date.toLocaleTimeString()
}
</script>
<template>
  <div style="max-width: 520px; padding-top: 1.25rem;">
    <div v-for="pokemon in pokemonList" class="card flex bg_white" :key="pokemon.entry_number">
      <div class="card_image">
        <PokemonImage :entry="pokemon.entry_number" />
      </div>
      <div class="card-info">
        <div class="card_title">
          <h1>
            {{
              pokemon.pokemon_species.name[0].toUpperCase() + pokemon.pokemon_species.name.slice(1)
            }}
          </h1>
          <span class="pokemon_id">ID: {{ pokemon.entry_number }}</span>
        </div>
        <div style="display: flex">
          <PokemonDetails :entry="pokemon.entry_number" />
          <PokemonStatus :species="pokemon" />
        </div>
        <div id="actions">
          <button class="button bg_purple" @click="handlePokemonCapture(pokemon)">
            {{ pokemon.isCaptured ? 'Release' : 'Catch!' }}
          </button>
          <button
            class="button"
            :class="{ bg_red: pokemon.isFavorite }"
            @click="toggleFavorite(pokemon)"
          >
            {{ pokemon.isFavorite ? 'Unfavorite' : 'Favorite' }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
.card .card_image {
  width: 40%;
}

.card_image img {
  width: 100%;
}

.card .card-info {
  width: 60%;
}

.card .card_title {
  display: flex;
  justify-content: space-between;
  border-bottom: 2px solid grey;
}

.card_title .pokemon_id {
  font-size: 1.75em;
}

.card h1 {
  font-size: 1.75em;
  margin: 0;
}

#actions .button {
  border-radius: 25px;
  padding: 0.5rem 1rem;
  cursor: pointer;
}

#actions .button + .button {
  margin-left: 0.5rem;
}
</style>
