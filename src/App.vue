<template>
  <div class="todos-bg-container">
    <div class="container">
      <div class="row">
        <div class="col-12">
          <h1 class="todos-heading">Todos</h1>
          <task-creation @add-task="addTask"></task-creation>
          <task-list :tasks="filteredTasks" @delete-task="deleteTask"></task-list>
          <task-filtering @filter-tasks="applyFilter"></task-filtering>
          <button class="button" @click="saveTodoList">Save</button>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import TaskCreation from './components/TaskCreation.vue';
import TaskList from './components/TaskList.vue';
import TaskFiltering from './components/TaskFiltering.vue'; // Import TaskFiltering component

export default {
  data() {
    return {
      todoList: [],
      selectedFilter: 'all',
    };
  },
  computed: {
    filteredTasks() {
      if (this.selectedFilter === 'all') {
        return this.todoList;
      } else if (this.selectedFilter === 'completed') {
        return this.todoList.filter(task => task.isChecked);
      } else if (this.selectedFilter === 'incomplete') {
        return this.todoList.filter(task => !task.isChecked);
      }
      return this.todoList; // Default return statement
    },
  },
  methods: {
    addTask(taskText) {
      this.todoList.push({ text: taskText, isChecked: false });
    },
    deleteTask(index) {
      this.todoList.splice(index, 1);
    },
    saveTodoList() {
      localStorage.setItem('todoList', JSON.stringify(this.todoList));
    },
    applyFilter(filter) {
      this.selectedFilter = filter;
    },
  },
  components: {
    TaskCreation,
    TaskList,
    TaskFiltering, // Register TaskFiltering component
  },
};
</script>

<style scoped>
.todos-bg-container {
    background-color: #f9fbfe;
    height: 100vh;
}

.todos-heading {
    text-align: center;
    font-family: "Roboto";
    font-size: 46px;
    font-weight: 500;
    margin-top: 20px;
    margin-bottom: 20px;
}

.create-task-heading {
    font-family: "Roboto";
    font-size: 32px;
    font-weight: 700;
}

.create-task-heading-subpart {
    font-family: "Roboto";
    font-size: 32px;
    font-weight: 500;
}

.todo-items-heading {
    font-family: "Roboto";
    font-size: 32px;
    font-weight: 700;
}

.todo-items-heading-subpart {
    font-family: "Roboto";
    font-size: 32px;
    font-weight: 500;
}

.todo-items-container {
    margin: 0;
    padding: 0;
}

.todo-item-container {
    margin-top: 15px;
}

.todo-user-input {
    background-color: white;
    width: 100%;
    border-style: solid;
    border-width: 1px;
    border-color: #e4e7eb;
    border-radius: 10px;
    margin-top: 10px;
    padding: 15px;
}

.button {
    color: white;
    background-color: #4c63b6;
    font-family: "Roboto";
    font-size: 18px;
    border-width: 0;
    border-radius: 4px;
    margin-top: 20px;
    margin-bottom: 50px;
    padding-top: 5px;
    padding-bottom: 5px;
    padding-right: 20px;
    padding-left: 20px;
}

.label-container {
    background-color: #e6f6ff;
    width: 100%;
    border-style: solid;
    border-width: 5px;
    border-color: #096f92;
    border-right: none;
    border-top: none;
    border-bottom: none;
    border-radius: 4px;
}

.checkbox-input {
    width: 20px;
    height: 20px;
    margin-top: 12px;
    margin-right: 12px;
}

.checkbox-label {
    font-family: "Roboto";
    font-size: 16px;
    font-weight: 400;
    width: 82%;
    margin: 0;
    padding-top: 10px;
    padding-bottom: 10px;
    padding-left: 20px;
    padding-right: 20px;
    border-radius: 5px;
}

.delete-icon-container {
    text-align: right;
    width: 18%;
}

.delete-icon {
    padding: 15px;
}

.checked {
    text-decoration: line-through;
}
</style>
