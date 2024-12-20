<template>
    <div class="app">
        <header class="header">
            <h1 id="header-title">Bookoria - Your Digital Bookshelf</h1>
        </header>
        <main class="container">
            <section class="form-section">
                <AddBook @add-book="addBook" />
            </section>
            <section class="filter-section flex items-center space-x-4">
                <BookFilter :filter-text="filterText"
                            :filter-author="filterAuthor"
                            :filter-state="filterState"
                            @update-filters="updateFilters" />
            </section>
            <section class="books-section">
                <!-- Display books only if the filter matches -->
                <BooksList :books="filteredBooks"
                           @remove-book="removeBook"
                           @update-book="updateBook"
                           v-if="filteredBooks.length > 0" />
                <!-- Show message only when no matching books -->
                <p v-else-if="(filterText || filterState !== 'All') && filteredBooks.length === 0" class="no-books">
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
    const filterAuthor = ref('');
    const filterState = ref('All');

    const addBook = (book) => {
        books.value.push(book);
    };

    const removeBook = (book) => {
        books.value = books.value.filter((b) => b !== book);
    };

    // Listen for filter updates from BookFilter
    const updateFilters = ({ text, author, state }) => {
        filterText.value = text;
        filterAuthor.value = author;
        filterState.value = state;
    };

    const filteredBooks = computed(() => {
        return books.value.filter((book) => {
            const matchesTitle = book.title.toLowerCase().includes(filterText.value.toLowerCase());
            const matchesAuthor = book.author?.toLowerCase().includes(filterAuthor.value.toLowerCase());
            const matchesState = filterState.value === 'All' || book.state === filterState.value;
            return matchesTitle && matchesAuthor && matchesState;
        });
    });

    const updateBook = (updatedBook) => {
        const index = books.value.findIndex((b) => b.title === updatedBook.title);
        if (index !== -1) {
            books.value[index] = updatedBook;
        }
    };
</script>

<style>
    /* Add your styles here */
    .app {
        font-family: 'Arial', sans-serif;
        padding: 20px;
        height: 100%;
        background-color: #f8f9fa;
        color: #333;
    }

    .header {
        background: linear-gradient(135deg, #C15F46, #5B211B);
        color: #ffffff;
        padding: 30px 20px;
        box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.3);
        text-align: center;
        margin: 0 auto;
        border-radius: 10px;
    }

    #header-title {
        font-size: 3rem;
        font-weight: bold;
        text-shadow: 1px 1px 3px #5D201C;
        text-align: center;
    }

    .form-section {
        background: #ffffff;
        padding: 15px;
        border-radius: 10px;
        box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.2);
    }

    .container {
        max-width: 1200px;
        margin: 0 auto;
    }

    .filter-section {
        background: linear-gradient(135deg, #C15F46, #5B211B);
        padding: 15px;
        border-radius: 8px;
        box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.2);
        margin-bottom: 20px;
    }

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