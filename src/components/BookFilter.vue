<template>
        <!-- Filter by Title -->
        <input v-model="localFilterText"
               @input="emitFilters"
               placeholder="Search by Title"
               class="filter-title border rounded-md p-2 w-80" />
        <!-- Filter by Author -->
        <input v-model="localFilterAuthor"
               @input="emitFilters"
               placeholder="Search by Author"
               class="filter-author border rounded-md p-2 w-80" />
        <!-- Filter by State -->
        <select v-model="localFilterState"
                @change="emitFilters"
                class="filter-state border rounded-md p-2 w-48">
            <option value="All">All</option>
            <option value="Want to Read">Want to Read</option>
            <option value="Reading">Reading</option>
            <option value="Finished">Finished</option>
        </select>
</template>

<script setup>
    import { ref, watchEffect } from 'vue';

    const props = defineProps({
        filterText: String,
        filterAuthor: String,
        filterState: String,
    });

    const emit = defineEmits(['update-filters']);

    const localFilterText = ref(props.filterText);
    const localFilterAuthor = ref(props.filterAuthor);
    const localFilterState = ref(props.filterState);

    const emitFilters = () => {
        emit('update-filters', {
            text: localFilterText.value,
            author: localFilterAuthor.value,
            state: localFilterState.value,
        });
    };

    // Sync local refs with props (in case props change from parent)
    watchEffect(() => {
        localFilterText.value = props.filterText;
        localFilterAuthor.value = props.filterAuthor;
        localFilterState.value = props.filterState;
    });
</script>

<style scoped>
    .filter-section {
        display: flex;
        align-items: center;
        gap: 1rem;
    }

    .filter-title, .filter-author, .filter-state {
        padding: 8px;
        font-size: 1rem;
        border-radius: 8px;
        border: 1px solid #ccc;
        transition: border-color 0.3s ease;
    }

        .filter-title:focus, .filter-author:focus, .filter-state:focus {
            border-color: #5B211B;
            outline: none;
        }
</style>