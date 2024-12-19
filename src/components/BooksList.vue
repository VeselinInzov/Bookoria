<template>
    <div class="books-list grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 xl:grid-cols-6 gap-x-60 gap-y-12 justify-items-center w-full">
        <BookCard v-for="(book, index) in books"
                  :key="index"
                  :book="book"
                  @delete-book="deleteBook"
                  @update-book="updateBook" />
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

    const emit = defineEmits(['remove-book', 'update-book']);

    const deleteBook = (book) => {
        emit('remove-book', book);
    };

    const updateBook = (book) => {
        emit('update-book', updateBook);
    };
</script>