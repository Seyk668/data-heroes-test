<script setup>
const props = defineProps({
  filters: {
    type: Object,
    required: true,
  }
});

const emits = defineEmits(['apply-filters']);
</script>

<template>
  <div class="filters">
    <div class="form-container">
      <input
          v-model="filters.name"
          id="name-input"
          type="text"
          class="form-control"
      />
      <label for="name-input" class="label">Имя</label>
    </div>
    <select v-model="filters.status">
      <option value="">Любой статус</option>
      <option value="alive">Живой</option>
      <option value="dead">Мертвый</option>
      <option value="unknown">Неизвестно</option>
    </select>
    <button @click="emits('apply-filters')" class="btn">Применить</button>
  </div>
</template>

<style scoped>
.filters {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 24px;
  gap: 20px;
}

.form-container {
  position: relative;
}
.form-control,
select {
  display: block;
  width: 100%;
  padding: 12px;
  border: 2px solid #DADDE2;
  border-radius: 16px;
  color: #181818;
  outline: none;
  transition: border-color .15s ease;
  word-break: break-word;
  -webkit-appearance: none;
  font-size: 1rem;
  line-height: 24px;
  overflow: visible;
  position: relative;
}
.label {
  display: block;
  padding: 0 .25rem;
  position: absolute;
  left: .75rem;
  top: .9375rem;
  background-color: #FFFFFF;
  font-size: 1rem;
  font-weight: 400;
  color: rgb(112,117,121);
  transition: transform .35s ease-out, color .35s ease-out;
  pointer-events: none;
  transform-origin: left center;
  white-space: nowrap;
  transform: scale(0.75) translate(-0.5rem, -2.25rem);
}
.form-control:focus,
.form-control:hover,
select:focus,
select:hover {
  border-color: #0084FF;
  caret-color: #0084FF;
}
.form-control:focus + label,
.form-control:hover + label {
  color: #0084FF;
}
select {
  width: fit-content;
  cursor: pointer;
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