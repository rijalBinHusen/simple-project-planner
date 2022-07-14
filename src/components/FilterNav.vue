<template>
    <nav class="filter-nav">
        <button @click="updateFilter('all')" :class="{ active: currentFilter == 'all' }">View all</button>
        <button @click="updateFilter('completed')" :class="{ active: currentFilter == 'completed' }">Completed</button>
        <button @click="updateFilter('ongoing')" :class="{ active: currentFilter == 'ongoing' }">On going</button>
    </nav>
</template>

<script>
export default {
    methods: {
        updateFilter(by) {
            this.$emit("filterChange", by)
        }
    },
    props: ['currentFilter'],
}
</script>

<style scoped>
    .filter-nav button {
        background: none;
        border: none;
        color: #bbb;
        outline: none;
        font-size: 12px;
        text-transform: uppercase;
        margin-right: 10px;
        letter-spacing: 1px;
        font-weight: bold;
        cursor: pointer;
    }
    .filter-nav button.active {
        color: #555;
    }
</style>