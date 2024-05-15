<template>
  <div class="app-card">
    <img :src="image" :alt="name">
    <div class="content">
      <h3>{{ name }}</h3>
      <p class="status">{{ `${status} - ${species}` }}</p>
      <div class="location">
        <p>Last known location:</p>
        <h4>{{ location }}</h4>
      </div>
      <div class="location">
        <p>First seen in:</p>
        <h4>{{ origin }}</h4>
      </div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  name: String,
  status: String,
  species: String,
  origin: String,
  location: String,
  image: String
})
</script>

<style src="@/assets/stylus/card.styl"></style>
