<template>
  <div>
    <label>Show:
      <select v-model="selectedFilter" @change="filterTasks">
        <option value="all">All</option>
        <option value="completed">Completed</option>
        <option value="incomplete">Incomplete</option>
      </select>
    </label>
    <i class="far fa-trash-alt delete-icon" @click="clearFilter"></i>
  </div>
</template>


<script>
export default {
  data() {
    return {
      selectedFilter: 'all',
    };
  },
  methods: {
    filterTasks() {
      this.$emit('filter-tasks', this.selectedFilter);
    },
    clearFilter() {
      this.selectedFilter = 'all'; // Reset the filter to 'All'
      this.$emit('filter-tasks', 'all'); // Emit 'All' as the selected filter
    },
  },
};
</script>

<style scoped>
/* Your existing CSS styles */

/* Style for the delete icon */
.delete-icon {
  font-size: 18px;
  color: #ff4136; /* You can choose your desired color */
  margin-left: 10px; /* Add some spacing between the select and delete icon */
  cursor: pointer;
}

/* Hover effect for the delete icon (optional) */
.delete-icon:hover {
  color: #e00;
}
</style>
