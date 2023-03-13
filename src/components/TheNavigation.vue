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
const { destinations } = defineProps(['destinations'])
</script>

<style scoped></style>
