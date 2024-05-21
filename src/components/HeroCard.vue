<script setup>
import axios from "axios";
import {onMounted, ref, watch} from "vue";

const props = defineProps({
  item: {
    type: Object,
    required: true,
  }
})

const episodeName = ref('');

function activeColor(item) {
  switch (item) {
    case "Alive":
      return "green";
    case "Dead":
      return "red";
    case "unknown":
      return "rgb(158, 158, 158)";
  }
}
const fetchEpisodeName = async (episodeUrl) => {
  try {
    const response = await axios.get(episodeUrl);
    episodeName.value = response.data.name;
  } catch (error) {
    console.error('Не удалось получить название эпизода:', error);
  }
};

onMounted(() => {
  fetchEpisodeName(props.item.episode[0]);
});
</script>

<template>
<div class="card">
  <div class="card-img" :style="{ backgroundImage: `url(${ item.image })`}"></div>
  <div class="card-body">
    <div class="info">
      <h2>{{ item.name }}</h2>
      <div class="status">
        <span class="dot" :style="{ background: activeColor(item.status) }"></span>
        {{ item.status }} - {{ item.species }}
      </div>
    </div>
    <div class="info">
      <div class="text-grey">Last known location:</div>
      <div class="text-link">{{ item.location.name }}</div>
    </div>
    <div class="info">
      <div class="text-grey">First seen in:</div>
      <div class="text-link">{{ episodeName }}</div>
    </div>
  </div>
</div>
</template>

<style scoped>
.card {
  width: 600px;
  height: 220px;
  display: flex;
  overflow: hidden;
  border-radius: 0.5rem;
  box-shadow: rgba(0, 0, 0, 0.1) 0 4px 6px -1px, rgba(0, 0, 0, 0.06) 0 2px 4px -1px;
  color: #ffffff;
  background: rgb(60, 62, 68);
}
.card-img {
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
  flex: 2 1 0;
  width: 100%;
}
.card-body {
  flex: 3 1 0;
  padding: 0.75rem;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
h2 {
  font-size: 1.5rem;
  font-weight: 700;
  line-height: 1.1;
}
.status {
  display: flex;
  align-items: center;
  font-size: 16px;
  font-weight: 500;
}
.dot {
  display: inline-block;
  height: 0.5rem;
  width: 0.5rem;
  margin-right: 0.375rem;
  border-radius: 50%;
  background: rgb(158, 158, 158);
}

.text-grey {
  color: rgb(158, 158, 158);
  font-size: 16px;
  font-weight: 500;
}
.text-link {
  color: rgb(245, 245, 245);
  font-size: 1.1rem;
}
</style>