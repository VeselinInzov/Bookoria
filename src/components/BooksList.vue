<template>
  <div class="books-list grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6 justify-center">
    <BookCard
      v-for="(book, index) in books"
      :key="index"
      :book="book"
      @delete-book="deleteBook"
    />
  </div>
</template>

<script setup>
import BookCard from './BookCard.vue';

const props = defineProps({
  books: {
    type: Array,
    required: true
  }
});

const emit = defineEmits(['remove-book']);

const deleteBook = (book) => {
  emit('remove-book', book);
};
</script>