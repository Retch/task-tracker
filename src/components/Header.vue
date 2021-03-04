<template>
  <header>
    <div class="row">
      <h3 class="col left-align">{{ title }}</h3>
      <Button class="col valign-wrapper" text="Add Task" color="green" />
    </div>
  </header>
</template>

<script>
import Button from "./Button.vue";

export default {
  name: "Header",
  props: {
    title: {
      type: String,
      default: "default title",
    },
  },
  components: {
    Button,
  },
};
</script>
