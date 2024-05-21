<script setup>
import { onMounted, ref } from "vue";
import axios from "axios";
import HeroCard from "@/components/HeroCard.vue";
import FiltersComponent from "@/components/FiltersComponent.vue";
import PaginationComponent from "@/components/PaginationComponent.vue";

const store = ref({ info: {}, results: [] });
const filters = ref({ name: '', status: '', page: 1 });

onMounted(() => {
  getData();
})

const getData = async () => {
  const { name, status, page } = filters.value;
  try {
    const response = await axios.get('https://rickandmortyapi.com/api/character', {
      params: {name, status, page}
    })
    store.value = response.data;
  } catch (error) {
    alert('Персонажа с таким именем не найдено')
    console.error(error);
  }
};

const applyFilters = () => {
  filters.value.page = 1;
  getData();
};

const changePage = (direction) => {
  if (direction === 'next' && store.value.info.next) {
    filters.value.page++;
  } else if (direction === 'prev' && store.value.info.prev) {
    filters.value.page--;
  }
  getData();
};
</script>

<template>
<div class="home-page">
  <FiltersComponent :filters="filters" @apply-filters="applyFilters"/>
  <div class="container">
    <HeroCard v-for="(item, index) in store.results" :key="index" :item="item" />
  </div>
  <PaginationComponent @change-page="changePage" />
</div>
</template>

<style scoped>
.container {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
  gap: 20px;
}
</style>