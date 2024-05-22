<template>
  <div class="app-button">
    <button
      :class="{ 'disabled-button': disabled }"
      :disabled="disabled"
    >
      {{ title }}
    </button>
  </div>
</template>
<script setup>
defineProps({
  title: String,
  disabled: {
    type: Boolean,
    default: false,
    required: false
  }
})
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
    &:hover {
      background-color gray
      color white
    }
  }
  .disabled-button {
    cursor not-allowed
    &:hover {
      background-color transparent
      color inherit
    }
  }
}
</style>
