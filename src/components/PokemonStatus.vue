<script setup>
import { ref } from 'vue'

const props = defineProps({
  species: Object
})

const pokemon = ref(props.species)

</script>
<template>
  <div id="status">
    <div v-if="pokemon.isFavorite" class="status_marker inline_img">
      <img src="/src/assets/star.webp" alt="Favorite" />
      <span>{{ pokemon.dateFavorited }}</span>
    </div>
    <div v-if="pokemon.isCaptured" class="status_marker inline_img">
      <img src="/src/assets/pokeball.webp" alt="Captured" />
      <span>{{ pokemon.dateCaptured }}</span>
    </div>
    <div v-if="!pokemon.isCaptured" class="status_marker inline_img">
      <span>{{ pokemon.dateReleased }}</span>
    </div>
  </div>
</template>
<style scoped>
#status {

}

.status_marker {
  display: flex;
  width: 128px;
  margin: 1.5em 0;
}

.status_marker img {
  margin-right: 0.5rem;
}
</style>
