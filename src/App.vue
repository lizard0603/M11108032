<template>
  <div id="app">
    <form v-on:submit.prevent="addNewTask">
      <label for="new-task">To-do list   </label>
      <input v-model="newTaskText" id="new-task" placeholder="輸入...">
      <button>新增</button>
    </form>
    <TasksList v-bind:tasks="tasks" v-on:delete-task="deleteTask"></TasksList>
  </div>
</template>

<script>
import TasksList from "./components/to-dolist";

export default {
  name: "App",
  components: {
    TasksList
  },
  data: () => ({
    newTaskText: "",
    tasks: [
      
    ]
  }),
  methods: {
    addNewTask() {
      const { newTaskText } = this;
      if (!newTaskText) {
        return;
      }
      this.tasks.push({ id: Math.random(), text: this.newTaskText });
      this.newTaskText = null;
    },
    deleteTask(taskId) {
      const remainingTasks = this.tasks.filter(task => task.id !== taskId);
      this.tasks = remainingTasks;
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
