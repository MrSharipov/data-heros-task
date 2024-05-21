<template>
  <div class="app-home-page">
    <header>
      <h1>The Rick and Morty</h1>
    </header>
    <section>
      <div class="settings">
        <div class="filters">
          <app-select-input
            v-model="statusValue"
            option-label="status"
            :options="statusSelectList"
          />
          <app-select-input
            v-model="nameValue"
            option-label="name"
            :options="nameSelectList"
          />
          <app-button @click="handleFilter" title="Apply" />
        </div>
        <div class="paginator">
          <app-paginator />
        </div>
      </div>
      <div class="gallery">
        <template v-if="characters && characters.length > 0">
          <app-card
            v-for="(character, index) in characters"
            :key="index"
            :name="character.name"
            :status="character.status"
            :species="character.species"
            :origin="character.origin.name"
            :location="character.location.name"
            :image="character.image"
          />
        </template>

        <h1 class="not-found" v-else>Not Found</h1>
      </div>
    </section>
  </div>
</template>
<script setup>
import AppCard from '@/components/AppCard.vue'
import { onMounted, ref } from 'vue'
import AppSelectInput from '@/components/AppSelectInput.vue'
import AppPaginator from '@/components/AppPaginator.vue'
import AppButton from '@/components/ui/AppButton.vue'

const statusValue = ref('')
const nameValue = ref('')
const characters = ref({})
const pagination = ref({
  count: 0,
  pages: 1,
  next: '#',
  prev: null
})

const statusSelectList = ref([
  {
    key: 'Alive',
    value: 'Alive'
  },
  {
    key: 'Unknown',
    value: 'unknown'
  },
  {
    key: 'Dead',
    value: 'Dead'
  }
])

const nameSelectList = ref([
  {
    key: 'Summer',
    value: 'summer'
  },
  {
    key: 'Jerry',
    value: 'jerry'
  },
  {
    key: 'Morty',
    value: 'morty'
  },
  {
    key: 'Agency',
    value: 'agency'
  }
])

const handleFilter = () => {
  getData(nameValue.value?.value, statusValue.value?.value)
}

const getData = (name = null, status = null) => {
  let url = 'https://rickandmortyapi.com/api/character?'
  name ? url += `name=${name}` : url
  status ? url += `&status=${status}` : url
  fetch(url).then((res) =>
    res.json().then((data) => {
      characters.value = data.results
      pagination.value = data.info
    })
  )
}

onMounted(() => {
  getData()
})
</script>
<style src="@/assets/stylus/home-page.styl"></style>
