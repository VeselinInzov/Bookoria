<template>
  <div class="filter p-4 bg-white rounded-lg shadow-md">
    <input
      v-model="filterValue"
      @input="updateFilter"
      placeholder="Filter by name"
      class="input w-full"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue';

const filterValue = ref('');
const emit = defineEmits(['update-filter']);
const updateFilter = () => {
  emit('update-filter', filterValue.value);
};
</script>

<style scoped>
.input {
  padding: 8px;
  font-size: 1rem;
  border-radius: 8px;
  border: 1px solid #ccc;
  transition: border-color 0.3s ease;
}

.input:focus {
  border-color: #4a90e2;
  outline: none;
}
</style>