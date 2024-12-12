<template>
  <div class="app">
    <header class="header">
      <h1>Bookoria - Your Digital Bookshelf</h1>
    </header>
    <main class="container">
      <section class="form-section">
        <AddBook @add-book="addBook" />
      </section>
      <section class="filter-section">
        <BookFilter @update-filter="filterBooks" />
      </section>
      <section class="books-section">
        <!-- Display books only if there are books available or if the filter matches -->
        <BooksList
          :books="filteredBooks"
          @remove-book="removeBook"
          v-if="filteredBooks.length > 0"
        />
        <!-- Show message only when there is a filter text and no matching books -->
        <p v-else-if="filterText && filteredBooks.length === 0" class="no-books">
          No books found!
        </p>
      </section>
    </main>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import AddBook from './components/AddBook.vue';
import BookFilter from './components/BookFilter.vue';
import BooksList from './components/BooksList.vue';

const books = ref([]);
const filterText = ref('');

const addBook = (book) => {
  books.value.push(book);
};

const removeBook = (book) => {
  books.value = books.value.filter((b) => b !== book);
};

const filterBooks = (filter) => {
  filterText.value = filter;
};

const filteredBooks = computed(() => {
  return books.value.filter((book) =>
    book.name.toLowerCase().includes(filterText.value.toLowerCase())
  );
});
</script>

<style>
/* Add your styles here */
.app {
  font-family: 'Arial', sans-serif;
  padding: 20px;
  background-color: #f8f9fa;
  color: #333;
}

.header h1 {
  font-size: 2rem;
  text-align: center;
  margin-bottom: 20px;
  color: #4a90e2;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
}

.form-section,
.filter-section,
.books-section {
  margin-bottom: 20px;
}

.no-books {
  font-size: 1.2rem;
  color: #888;
  text-align: center;
  padding: 20px;
}
</style>