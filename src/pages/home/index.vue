<template>
  <div class="app-home-page">
    <header>
      <h1>The Rick and Morty</h1>
    </header>
    <section>
      <div class="settings">
        <div class="filters">
          <app-select-input />
          <app-select-input />
          <button>Apply</button>
        </div>
        <div class="paginator">
          <button>Prev</button>
          <p>Current page: 1</p>
          <p>All pages: 48</p>
          <button>Next</button>
        </div>
      </div>
      <div class="gallery">
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
      </div>
    </section>
  </div>
</template>
<script setup>
import AppCard from '@/components/AppCard.vue';
import { onMounted, ref } from 'vue';
import AppSelectInput from '@/components/AppSelectInput.vue';

const characters = ref({});
const pagination = ref({
  count: 0,
  pages: 1,
  next: '#',
  prev: null
});

const getData = () => {
  fetch('https://rickandmortyapi.com/api/character').then((res) =>
    res.json().then((data) => {
      characters.value = data.results;
      pagination.value = data.info;
    })
  );
};

onMounted(() => {
  getData();
});
</script>
<style src="@/assets/stylus/home-page.styl"></style>
