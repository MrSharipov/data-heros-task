<template>
  <div class="app-paginator">
    <app-button title="Prev" />
    <p>1 out of 48</p>
    <app-button title="Next" />
  </div>
</template>
<script setup lang="ts">
import AppButton from '@/components/ui/AppButton.vue';
</script>

<style lang="stylus" scoped>
.app-paginator {
  display flex
  align-items center
  gap 1rem
}
</style>
