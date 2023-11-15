<script setup>
import axios from 'axios';

axios.get('https://pokeapi.co/api/v2/pokemon?offset=0')
  .then(res => res.data)
</script>

<template>
  <main>
    <p>{{ hello }}</p>
  </main>
</template>
