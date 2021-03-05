<template>
  <header>
    <div class="container">
      <div class="row">
        <h4 class="col">{{ title }}</h4>
        <Button
          v-show="homePage"
          @btn-click="$emit('show-add-task')"
          class="col right"
          :text="showaddtask ? 'close' : 'add'"
        />
      </div>
    </div>
  </header>
</template>

<script>
import Button from "./Button.vue";

export default {
  name: "Header",
  props: {
    title: String,
    showaddtask: Boolean,
  },
  components: {
    Button,
  },
  computed: {
    homePage() {
      if (this.$route.path === "/") {
        return true;
      } else {
        return false;
      }
    },
  },
};
</script>
