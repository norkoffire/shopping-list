<script setup>
import { ref } from 'vue'

const items = ref([
  { id: 1, label: 'toto' },
  { id: 2, label: 'tata' },
  { id: 3, label: 'titi' },
  { id: 4, label: 'heyy' },
])
</script>

<template>
  <ul>
    <li v-for="{ id, label } in items" :key="id">
      {{ label }}
    </li>
  </ul>
</template>
