<script setup>
import { ref } from 'vue'

const isMouseHold = ref(false)

const props = defineProps({
  captive: Object
})

function startHold() {
  if (props.captive.isCaptured) {
    releasePokemon(props.captive)
  }

  isMouseHold.value = true
  setTimeout(() => {
    if (isMouseHold.value) {
      catchPokemon(props.captive)
    }
  }, 3000)
}

function stopHold() {
  isMouseHold.value = false
}

function catchPokemon(pokemon) {
  pokemon.isCaptured = true
  const date = new Date()
  pokemon.dateCaptured = date.toLocaleDateString() + ' ' + date.toLocaleTimeString()
}

function releasePokemon(pokemon) {
  pokemon.isCaptured = false
  const date = new Date()
  pokemon.dateReleased = date.toLocaleDateString() + ' ' + date.toLocaleTimeString()
  return
}
</script>
<template>
  <button class="button bg_purple" @mousedown="startHold" @mouseup="stopHold" @mouseleave="stopHold">
    {{ props.captive.isCaptured ? 'Release' : 'Catch!' }}
  </button>
</template>
<style scoped></style>
