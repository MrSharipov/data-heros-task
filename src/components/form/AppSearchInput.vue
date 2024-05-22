<template>
  <div class="app-search-input">
    <input
      type="search"
      v-model="input"
      :placeholder="placeHolder"
      @input="handleInput"
      :style="{
        backgroundImage: !input ? searchIconUrl: 'none'
      }"
    />
    <app-icon
      v-if="input"
      class="clearInput"
      icon="cross"
      size=".8rem"
      @click="clearInput"
    />
  </div>
</template>
<script setup>
import { ref } from 'vue'
import AppIcon from '@/components/ui/AppIcon.vue'

const props = defineProps({
  modelValue: {
    type: String,
    required: true
  },
  placeHolder: {
    type: String,
    required: false,
    default: 'Search...'
  }
})

const searchIconUrl = "url('/public/images/search.svg')"
const emit = defineEmits(['update:modelValue'])
const input = ref(props.modelValue)

const clearInput = () => {
  input.value = '';
  emit('update:modelValue', input.value)
}
const handleInput = () => {
  emit('update:modelValue', input.value)
}
</script>
<style src="@/assets/stylus/search-input.styl"></style>