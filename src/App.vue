<script setup>
import { RouterView } from 'vue-router';
import TheNav from '@/components/TheNav.vue';
</script>

<template>
  <div class="app">
    <the-nav />
    <RouterView />
  </div>
</template>

<style src="@/assets/stylus/app.styl"></style>
