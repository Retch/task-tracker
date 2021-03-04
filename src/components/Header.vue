<template>
  <header>
    <div class="row">
      <h3 class="col left-align">{{ title }}</h3>
      <Button
        @show-add-task="$emit('show-add-task')"
        class="col valign-wrapper"
        :text="showaddtask ? 'Close' : 'Add Task'"
        color="green"
      />
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
};
</script>
