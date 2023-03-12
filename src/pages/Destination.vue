<template>
  <section v-if="destination.data" class="destination">
    <h1>{{ destination.data.name }}</h1>
    <div class="destination-details">
      <img
        :src="`/images/${destination.data.image}`"
        :alt="destination.data.name"
      />
      <p>{{ destination.data.description }}</p>
    </div>
  </section>
</template>

<script setup>
import { onMounted, reactive, watch } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()

const destination = reactive({
  data: null,
  error: null,
  loading: false,
})

const fetchData = async () => {
  destination.loading = true

  try {
    const response = await fetch(
      proxyUrl + `https://travel-dummy-api.netlify.app/${route.params.slug}`
    )
    const data = await response.json()
    destination.data = data
  } catch (error) {
    destination.error = error
  } finally {
    destination.loading = false
  }
}
onMounted(() => {
  fetchData()
})
watch(
  () => route.params.id,
  async () => {
    await fetchData()
  }
)
</script>

<style lang="scss" scoped></style>
