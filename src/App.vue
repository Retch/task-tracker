<template>
  <div class="container">
    <Header
      @show-add-task="toggleAddTask"
      class="col s6"
      title="Task Tracker"
      :showaddtask="showaddtask"
    />

    <router-view @show-add-task="toggleAddTask" :showaddtask="showaddtask"></router-view>
    <Footer />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";

export default {
  name: "App",
  components: {
    Header,
    Footer,
  },
  data() {
    return {
      showaddtask: false,
    };
  },
  methods: {
    toggleAddTask() {
      this.showaddtask = !this.showaddtask;
    },
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
