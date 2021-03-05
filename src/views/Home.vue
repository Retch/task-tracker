<template>
  <AddTask v-show="showaddtask" @add-task="addTask" />
  <Tasks
    @toggle-reminder="toggleReminder"
    @delete-task="deleteTask"
    class="col s6"
    :tasks="tasks"
  />
</template>

<script>
import Tasks from "../components/Tasks.vue";
import AddTask from "../components/AddTask.vue";

export default {
  name: "Home",
  props: {
    showaddtask: Boolean,
  },
  components: {
    Tasks,
    AddTask,
  },
  emits: {},
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
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

      this.$emit("show-add-task");
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
  emits: ["show-add-task"],
};
</script>
