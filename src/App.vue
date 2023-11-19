<script setup>
import { ref, reactive } from 'vue'
import PokemonEntries from './components/PokemonEntries.vue'

const title = ref('PokeDéx Web')

const sortOption = ref('')
const pokemonTypesList = ref([
  'normal',
  'fighting',
  'flying',
  'poison',
  'ground',
  'rock',
  'bug',
  'ghost',
  'steel',
  'fire',
  'water',
  'grass',
  'electric',
  'psychic',
  'ice',
  'dragon',
  'dark',
  'fairy',
  'unknown',
  'shadow'
])

const filteredTypes = reactive({
  firstType: '',
  secondType: ''
})

const filterName = ref('')
</script>

<template>
  <div class="bg_dark app-container">
    <div class="title">
      <img src="/src/assets/pokeball.webp" alt="" class="inline_img" />
      <h1>{{ title }}</h1>
      <img src="/src/assets/pokeball.webp" alt="" class="inline_img" />
    </div>
    <h3 style="text-align: center">Click and hold the 'Catch!' button to capture Pokémon!</h3>
    <div class="pokedex">
      <div style="position: relative; top: 0">
        <div style="position: sticky; padding-top: 1.25rem; top: 0">
          <div class="card bg_white">
            <span>Sort By:</span>
            <input type="radio" id="sortOption1" value="id" v-model="sortOption" checked />
            <label for="sortOption1">ID</label>
            <input type="radio" id="sortOption2" value="name" v-model="sortOption" />
            <label for="sortOption2">Name</label>

            <p>Select up to 2 types</p>
            <div class="flex">
              <select v-model="filteredTypes.firstType">
                <option value="" disabled>--SELECT--</option>
                <option v-for="type in pokemonTypesList" :value="type" :key="type">
                  {{ type[0].toUpperCase() + type.slice(1) }}
                </option>
              </select>
              <select v-model="filteredTypes.secondType">
                <option value="" disabled>--SELECT--</option>
                <option v-for="type in pokemonTypesList" :value="type" :key="type">
                  {{ type[0].toUpperCase() + type.slice(1) }}
                </option>
              </select>
            </div>

            <input type="text" v-model="filterName" placeholder="Search Pokemon...">
          </div>
        </div>
      </div>

      <PokemonEntries :sortBy="sortOption" :filter="filterName"/>
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

.pokedex {
  margin: 0 auto;
  max-width: 520px;
}

.title h1 {
  width: fit-content;
  margin: 0 1rem;
}

#searchPokemonByTypes input,
#searchPokemonByTypes select {
  display: block;
}

label {
  margin-bottom: 0.75em;
}

@media (width > 768px) {
  .pokedex {
  display: flex;
  justify-content: center;
  max-width: 1180px;
}
}
</style>
