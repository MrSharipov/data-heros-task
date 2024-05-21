<template>
  <div class="app-button">
    <button>{{ title }}</button>
  </div>
</template>
<script setup>
defineProps({
  title: String
});
</script>

<style lang="stylus" scoped>
.app-button {
  button {
    cursor pointer
    border 1px solid gray
    background-color transparent
    padding 8px
    border-radius 6px
    width 6rem
    &:hover{
      background-color gray
      color white
    }
  }
}
</style>
