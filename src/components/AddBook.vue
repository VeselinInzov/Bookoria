<template>
  <div class="add-book p-6 bg-white rounded-lg shadow-lg">
    <form @submit.prevent="submitBook" class="flex flex-col gap-4">
      <input v-model="name" placeholder="Book Name" class="input" required />
      <input v-model="image" placeholder="Image URL" class="input" required />
      <textarea v-model="description" placeholder="Description" class="input" required></textarea>
      <button
        type="submit"
        class="btn bg-blue-600 text-white py-2 px-6 rounded-md hover:bg-blue-700"
      >
        Add Book
      </button>
    </form>
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