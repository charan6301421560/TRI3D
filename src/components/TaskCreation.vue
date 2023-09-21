<!-- TaskCreation.vue -->
<template>
  <div>
    <input v-model="newTask" placeholder="What needs to be done?" @keyup.enter="addNewTask">
    <button class="button" @click="addNewTask">Add</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
    };
  },
  methods: {
    addNewTask() {
      if (this.newTask.trim() !== '') {
        this.$emit('add-task', this.newTask);
        this.newTask = '';
      }
    },
  },
};
</script>
