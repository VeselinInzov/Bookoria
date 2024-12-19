<template>
    <div>
        <div class="flex flex-wrap space-x-4 items-center">
            <form @submit.prevent="submitBook" class="flex space-x-4">
                <input v-model="name" placeholder="Book Name" class="input border rounded-md p-2 w-64" required />
                <input v-model="image" placeholder="Image URL" class="input border rounded-md p-2 w-64" />
                <input v-model="description" placeholder="Description" class="input border rounded-md p-2 w-64" required />
                <select v-model="state" class="input border rounded-md p-2 w-40" required>
                    <option value="Reading">Reading</option>
                    <option value="Finished">Finished</option>
                    <option value="Want to Read">Want to Read</option>
                </select>
                <button type="submit"
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
    const state = ref('Reading'); // Default state

    const emit = defineEmits(['add-book']);
    const submitBook = () => {
        const newBook = {
            name: name.value,
            image: image.value,
            description: description.value,
            state: state.value
        };
        emit('add-book', newBook);
        name.value = '';
        image.value = '';
        description.value = '';
        state.value = 'Reading';
    };
</script>


<style scoped>
    .input {
        border: 1px solid #C07764;
        padding: 10px;
        border-radius: 5px;
    }

    .btn {
        background-color: #5D201C;
        color: #ffffff;
        font-weight: bold;
        padding: 10px 20px;
        border-radius: 5px;
        cursor: pointer;
        transition: background-color 0.3s ease, color 0.3s ease;
    }

    .btn:hover {
        background-color: #C07764;
        color: #ffffff;
    }
</style>