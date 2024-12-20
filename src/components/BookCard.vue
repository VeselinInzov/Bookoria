<template>
    <div class="book-card bg-white rounded-lg shadow-lg p-6 flex flex-col items-center transition-transform hover:scale-105">
        <img :src="book.image || 'src/images/book-default.png'"
             alt="Book Cover"
             class="book-image rounded-md w-48 h-72 object-cover mb-4" />
        <h3 class="font-semibold text-2xl text-center mb-2">{{ book.title }}</h3>
        <p class="text-gray-700 text-center mb-4">{{ book.description }}</p>

        <!-- Dropdown for changing the book's state -->
        <select v-model="book.state"
                @change="updateBookState"
                class="state-dropdown border rounded-md p-2 w-full mb-4 text-center">
            <option value="Want to Read">Want to Read</option>
            <option value="Reading">Reading</option>
            <option value="Finished">Finished</option>
        </select>

        <button @click="deleteBook"
                class="btn bg-red-600 text-white py-2 px-6 rounded-md hover:bg-red-700 w-full">
            Delete
        </button>
    </div>
</template>

<script setup>
    import { computed, ref } from 'vue';

    const props = defineProps({
        book: {
            type: Object,
            required: true
        }
    });

    const emit = defineEmits(['delete-book', 'update-book']);

    // Local state to track dropdown selection
    const bookState = ref(props.book.state);

    const deleteBook = () => {
        emit('delete-book', props.book);
    };

    // Emit updated book state to the parent component
    const updateBookState = () => {
        emit('update-book', props.book);
    };
</script>

<style scoped>
    .book-card {
        width: 200px;
        background-color: #fff;
        border-radius: 8px;
        box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
        overflow: hidden;
        transition: transform 0.3s ease, box-shadow 0.3s ease;
    }

        .book-card:hover {
            transform: translateY(-4px);
            box-shadow: 0 8px 18px rgba(0, 0, 0, 0.15);
        }

    .book-cover {
        height: 300px;
        overflow: hidden;
    }

    .cover-image {
        width: 100%;
        height: 100%;
        object-fit: cover;
    }

    .book-info {
        padding: 16px;
    }

    .book-title {
        font-size: 1.1rem;
        font-weight: 600;
        color: #333;
        margin-bottom: 8px;
    }

    .book-description {
        font-size: 0.9rem;
        color: #555;
        margin-bottom: 12px;
    }

    .book-actions {
        display: flex;
        justify-content: flex-end;
    }

    .btn {
        background-color: #c15f46;
        color: white;
        padding: 6px 12px;
        border-radius: 6px;
        font-size: 0.8rem;
    }

        .btn:hover {
            background-color: #d32f2f;
        }

    .state-dropdown {
        font-size: 0.9rem;
        padding: 10px;
        text-align: center;
        border: 1px solid #d32f2f;
        border-radius: 5px;
        width: 100%;
        background-color: #fff;
    }

        .state-dropdown:focus {
            outline: none;
            border-color: #d32f2f;
        }
</style>