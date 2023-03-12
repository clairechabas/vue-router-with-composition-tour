<template>
  <nav id="nav">
    <router-link to="/">Home</router-link>
    <router-link
      v-for="destination in destinations"
      :to="{
        name: 'destination-page',
        params: { id: destination.id, slug: destination.slug },
      }"
      :key="destination.id"
    >
      {{ destination.name }}
    </router-link>
  </nav>
</template>

<script setup>
import { computed } from 'vue'
import data from '@/data.json'

const destinations = computed(() => data.destinations)
</script>

<style scoped></style>
