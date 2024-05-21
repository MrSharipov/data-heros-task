<template>
  <div class="app-icon">
    <i :class="`fi fi-${type}-${icon}`"></i>
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
    default:'rr'
  }
})
</script>

<style lang="stylus" scoped>
.app-icon {
  i{
    font-size 1rem
  }
}
</style>