<template>
  <ul class="todo-items-container">
    <li v-for="(task, index) in tasks" :key="index" :class="{ checked: task.isChecked }">
      <input type="checkbox" v-model="task.isChecked">
      <label :class="{ checked: task.isChecked }">{{ task.text }}</label>
      <i class="far fa-trash-alt delete-icon" @click="deleteTask(index)"></i>
    </li>
  </ul>
</template>


<script>
export default {
  props: {
    tasks: Array,
  },
  methods: {
    deleteTask(index) {
      this.$emit('delete-task', index);
    },
  },
};
</script>

<style scoped>
/* Your existing CSS styles */

/* Style for the checked (strikethrough) text */
.checked {
  text-decoration: line-through;
}

/* Style for the delete icon */
.delete-icon {
  font-size: 18px; /* Adjust the size as needed */
  color: #ff4136; /* You can choose your desired color */
  margin-left: 10px; /* Add some spacing between the text and the icon */
  cursor: pointer;
}

/* Hover effect for the delete icon (optional) */
.delete-icon:hover {
  color: #e00;
}
</style>
