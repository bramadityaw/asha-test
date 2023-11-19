<script setup>
import { onMounted, reactive, computed } from 'vue'
import PokemonImage from './PokemonImage.vue'
import PokemonDetails from './PokemonDetails.vue'
import PokemonStatus from './PokemonStatus.vue'
import CatchButton from './CatchButton.vue'

const props = defineProps({
  sortBy: String,
  filter: String,
})

const pokemonData = reactive({
  list: [],
  sortedList: computed(() => {
    let sortedList = [...pokemonData.list]

    if (props.sortBy === 'id') {
      sortedList.sort((a, b) => a.entry_number - b.entry_number)
    }

    if (props.sortBy === 'name') {
      sortedList.sort((a, b) => {
        const nameA = a.pokemon_species.name.toUpperCase()
        const nameB = b.pokemon_species.name.toUpperCase()
        return nameA.localeCompare(nameB)
      })
    }

    if (props.filter.length > 0) {
      sortedList = sortedList.filter(pokemon => pokemon.pokemon_species.name.includes(props.filter))
    }

    return sortedList
  })
})

onMounted(async () => {
  const pokedexData = await fetch('https://pokeapi.co/api/v2/pokedex/1').then((response) =>
    response.json()
  )

  pokemonData.list = pokedexData.pokemon_entries.map((pokemon) => ({
    ...pokemon,
    isFavorite: false,
    dateFavorited: '',
    isCaptured: false,
    dateCaptured: '',
    dateReleased: '',
    types: []
  }))
})

function toggleFavorite(pokemon) {
  pokemon.isFavorite = !pokemon.isFavorite
  if (pokemon.isFavorite) {
    const date = new Date()
    pokemon.dateFavorited = date.toLocaleDateString() + ' ' + date.toLocaleTimeString()
  }
}
</script>
<template>
  <div style="padding-top: 1.25rem; min-width: 440px;">
    <div
      v-for="pokemon in pokemonData.sortedList"
      class="card flex bg_white"
      :key="pokemon.entry_number"
    >
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
          <CatchButton :captive="pokemon"/>
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
