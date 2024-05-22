<template>
  <div class="app-home-page">
    <header>
      <h1>The Rick and Morty</h1>
    </header>
    <section>
      <div class="settings">
        <div class="filters">
          <app-search-input
            v-model="searchedName"
          />
          <app-select-input
            v-model="statusValue"
            option-label="status"
            :options="statusSelectList"
          />
          <app-button @click="handleFilter" title="Apply" />
        </div>
        <div class="paginator">
          <app-paginator
            :pagination
            @next="getData"
            @prev="getData"
          />
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
import AppSelectInput from '@/components/form/AppSelectInput.vue'
import AppPaginator from '@/components/AppPaginator.vue'
import AppButton from '@/components/ui/AppButton.vue'
import AppSearchInput from '@/components/form/AppSearchInput.vue'

const searchedName = ref('')
const statusValue = ref('')
const characters = ref({})
const pagination = ref({
  count: 0,
  pages: 1,
  current: 1,
  next: '#',
  prev: null
})

const updatePagination = (data) => {
  pagination.value = data;
  if (data.prev === null) {
    pagination.value.current =  1;
  } else if (data.next) {
    pagination.value.current = parseInt(data.next.split('page=')[1].charAt(0))-1;
  } else {
    return data.pages
  }
}

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
const url = ref('https://rickandmortyapi.com/api/character?')

const handleFilter = () => {
  getData(`${url.value}${searchedName.value ? `name=${searchedName.value}` : ''}${statusValue.value?.value ? `status=${statusValue.value?.value}` : ''}`)
}

const getData = (fetchUrl) => {
  fetch(fetchUrl).then((res) =>
    res.json().then((data) => {
      characters.value = data.results
      updatePagination(data.info)
    })
  )
}

onMounted(() => {
  getData(url.value)
})
</script>
<style src="@/assets/stylus/home-page.styl"></style>
