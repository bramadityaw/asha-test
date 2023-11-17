<script setup>
import { ref, onMounted } from 'vue'
import PokemonImage from './PokemonImage.vue'
import PokemonDetails from './PokemonDetails.vue'

const pokemonList = ref([])

onMounted(async () => {
  const pokedexData = await fetch('https://pokeapi.co/api/v2/pokedex/1').then((response) =>
    response.json()
  )

  pokemonList.value = pokedexData.pokemon_entries.map((pokemon) => ({
    ...pokemon,
    isFavorite: false,
    dateFavorited: Date
  }))
})

function toggleFavorite(pokemon) {
  pokemon.isFavorite = !pokemon.isFavorite
  const date = new Date()
  pokemon.dateFavorited = date.toLocaleDateString() + ' ' + date.toLocaleTimeString()
}
</script>
<template>
  <div style="columns: 2; max-width: 1020px; margin: 0 auto">
    <div v-for="pokemon in pokemonList" class="card bg-white" :key="pokemon.entry_number">
      <div class="card_image">
        <PokemonImage :entry="pokemon.entry_number"></PokemonImage>
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
          <PokemonDetails :entry="pokemon.entry_number"></PokemonDetails>
          <div v-if="pokemon.isFavorite" class="fav_marker inline_img">
            <img src="/src/assets/star.webp" alt="Favorite" />
            <span>{{ pokemon.dateFavorited }}</span>
          </div>
        </div>
        <div id="actions">
          <button class="button bg_purple">Catch!</button>
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
.card {
  min-height: 178px;
  min-width: 240px;
  border-radius: 25px;
  border: 2px solid grey;
  padding: 1rem;
  margin: 0 0.5rem 0.75rem;
  display: flex;
}

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
}

.card h2 {
  font-size: 1.5em;
}

.card h3 {
  font-size: 1.25em;
}

#actions .button {
  border-radius: 25px;
  padding: 0.5rem 1rem;
  cursor: pointer;
}

#actions .button + .button {
  margin-left: 0.5rem;
}

.bg-white {
  background-color: white;
  color: black;
}

.fav_marker {
  display: flex;
  width: 128px;
  margin-top: 1em;
}

.fav_marker img {
  margin-right: 0.5rem;
}
</style>
