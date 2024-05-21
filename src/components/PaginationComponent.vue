<script setup>
const emits = defineEmits(['change-page']);
</script>

<template>
  <div class="pagination">
    <button @click="emits('change-page','prev')" class="btn">Предыдущая</button>
    <button @click="emits('change-page','next')" class="btn">Следующая</button>
  </div>
</template>

<style scoped>
.pagination {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 24px;
  gap: 20px;
}
.btn {
  color: #ffffff;
  background-color: #0084ff;
  transition: all 0.3s ease-in-out;
  border: none;
  border-radius: 16px;
  padding: 16px 24px;
  width: fit-content;
  font-size: 16px;
  font-weight: 600;
  white-space: nowrap;
  cursor: pointer;
}

.btn:hover {
  background-color: #0070d9;
}
</style>