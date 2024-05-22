<template>
  <div
    class="app-select-input"
    ref="selectElementRef"
  >
    <label for="selectEl">{{ label }}</label>
    <div id="selectEl" class="select-wrapper">
      <div
        class="selected-option"
        :style="`width: ${width}`"
        @click="()=> isOptionVisible = true"
      >
        {{ mappedSelectedOption }}
        <app-icon
          v-if="selectedOption && clearable"
          icon="cross"
          @click="clearSelectedOption"
        />
        <app-icon v-else icon="filter" />
      </div>
      <Transition>
        <div
          v-if="isOptionVisible && options.length > 0"
          class="option-wrapper">
          <div
            class="option"
            v-for="(option, i) in options"
            :key="i"
            @click="()=>toggleOptionSelect(option)"
          >
            {{ option?.key || option }}
          </div>
        </div>
      </Transition>
    </div>
  </div>
</template>
<script setup lang="ts">
import { computed, onBeforeUnmount, onMounted, ref } from 'vue'
import AppIcon from '@/components/ui/AppIcon.vue'

const props = defineProps({
  label: {
    type: String,
    required: false
  },
  optionLabel: {
    type: String,
    required: false,
    default: 'item'
  },
  options: {
    type: Array,
    required: true
  },
  modelValue: {
    default: null
  },
  width: {
    type: String,
    default: '12rem'
  },
  clearable: {
    type: Boolean,
    default: true
  }
})
const selectedOption = ref(props.modelValue)
const isOptionVisible = ref(false)
const selectElementRef = ref(null)

const emit = defineEmits(['update:modelValue'])

const mappedSelectedOption = computed(() => {
  return selectedOption.value?.key || selectedOption.value?.key || `Select ${props.optionLabel}...`
})
const toggleOptionSelect = (option) => {
  selectedOption.value = option
  emit('update:modelValue', option)
  isOptionVisible.value = false
}

const closeOptionSelect = (element) => {
  if (!selectElementRef.value.contains(element?.target)) {
    setTimeout(() => {
      isOptionVisible.value = false
    }, 1)

  }
}

const clearSelectedOption = () => {
  selectedOption.value = null
  emit('update:modelValue', null)
}

onMounted(() => {
  window.addEventListener('click', closeOptionSelect)
})

onBeforeUnmount(() => {
  window.removeEventListener('click', closeOptionSelect)
})
</script>

<style src="@/assets/stylus/select-input.styl">


</style>
