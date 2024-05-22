<template>
  <div class="app-icon">
    <i
      :class="`fi fi-${type}-${icon}`"
      :style="`font-size: ${size}`"
    ></i>
  </div>
</template>
<script setup lang="ts">
defineProps({
  icon: {
    type: String,
    required: true
  },
  type: {
    type: String,
    required: false,
    default: 'rr'
  },
  size: {
    type: String,
    required: false,
    default: '1rem'
  }
})
</script>

<style></style>