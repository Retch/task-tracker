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
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: !task.reminder } : task
      );
    },
    addTask(task) {
      this.tasks = [...this.tasks, task];
      this.showaddtask = false;
    },
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text:
          "Appointment with doctor Fugiat fugiat cillum sit et in magna ad et mollit ea. Duis exercitation cupidatat quis ad.",
        day: "March 1st 12:30",
        reminder: false,
      },
      {
        id: 2,
        text: "Appointment in school",
        day: "Mai 1st 10:55",
        reminder: false,
      },
      {
        id: 3,
        text: "Appointment at work",
        day: "March 18 08:10",
        reminder: true,
      },
    ];
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
