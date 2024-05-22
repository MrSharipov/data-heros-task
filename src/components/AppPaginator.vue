<template>
  <div class="app-paginator">
    <app-button
      title="Prev"
      :disabled="!pagination?.prev"
      @click="prevAction"
    />
    <p>{{pagination?.current}} out of {{ pagination?.pages }}</p>
    <app-button
      title="Next"
      :disabled="!pagination?.next"
      @click="nextAction"
    />
  </div>
</template>
<script setup lang="ts">
import AppButton from '@/components/ui/AppButton.vue'

const props = defineProps({
  pagination: {
    type: Object,
    required: true
  }
})

const emit = defineEmits(['next', 'prev'])

const nextAction = () => {
  emit('next', props.pagination.next);
}

const prevAction = () => {
  emit('next', props.pagination.prev);
}
</script>

<style lang="stylus" scoped>
.app-paginator {
  display flex
  align-items center
  gap 1rem
}
</style>
