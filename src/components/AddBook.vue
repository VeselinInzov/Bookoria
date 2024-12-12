<template>
<div class="mb-8">
      <h2 class="text-xl font-bold mb-4">Add New Book</h2>
      <div class="flex space-x-4">
    <form @submit.prevent="submitBook" class="flex space-x-4">
      <input v-model="name" placeholder="Book Name" class="input border rounded-md p-2 w-80" required />
      <input v-model="image" placeholder="Image URL" class="input border rounded-md p-2 w-80" required />
      <input v-model="description" placeholder="Description" class="input border rounded-md p-2 w-80" required />
      <button
        type="submit"
        class="btn bg-blue-500 text-white py-2 px-6 rounded-md hover:bg-blue-600">
        Add Book
      </button>
    </form>
  </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const name = ref('');
const image = ref('');
const description = ref('');

const emit = defineEmits(['add-book']);
const submitBook = () => {
  const newBook = { name: name.value, image: image.value, description: description.value };
  emit('add-book', newBook);
  name.value = '';
  image.value = '';
  description.value = '';
};
</script>

<style scoped>
.input {
  padding: 10px;
  font-size: 1rem;
  border-radius: 8px;
  border: 1px solid #ccc;
}

.btn {
  padding: 10px;
  font-size: 1rem;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}
</style>