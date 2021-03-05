<template>
  <div class="container">
    <Header
      @show-add-task="toggleAddTask"
      class="col s6"
      title="Task Tracker"
      :showaddtask="showaddtask"
    />
    <div v-show="showaddtask">
      <AddTask @add-task="addTask" />
    </div>
    <Tasks
      @toggle-reminder="toggleReminder"
      @delete-task="deleteTask"
      class="col s6"
      :tasks="tasks"
    />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Tasks from "./components/Tasks.vue";
import AddTask from "./components/AddTask.vue";

export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [],
      showaddtask: false,
    };
  },
  methods: {
    toggleAddTask() {
      this.showaddtask = !this.showaddtask;
    },
    async deleteTask(id) {
      const res = await fetch(`api/tasks/${id}`, {
        method: "DELETE",
      });

      if (res.status === 200) {
        this.tasks = this.tasks.filter((task) => task.id !== id);
      } else {
        alert("Error deleting Task");
      }
    },
    async toggleReminder(id) {
      const tasktotoggle = await this.fetchTask(id);
      const updatetask = { ...tasktotoggle, reminder: !tasktotoggle.reminder };

      const res = await fetch(`api/tasks/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(updatetask),
      });

      const data = await res.json();

      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: data.reminder } : task
      );
    },
    async addTask(task) {
      const res = await fetch("api/tasks", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(task),
      });

      const data = await res.json();

      this.tasks = [...this.tasks, data];
      this.showaddtask = false;
    },
    async fetchTasks() {
      const res = await fetch("api/tasks");

      const data = res.json();

      return data;
    },
    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`);

      const data = res.json();

      return data;
    },
  },
  async created() {
    this.tasks = await this.fetchTasks();
  },
};
</script>

<style>
#Aapp {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
