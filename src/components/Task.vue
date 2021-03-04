<template>
  <div class="col s12 m6">
    <div class="card blue-grey darken-1">
      <div class="card-content white-text">
        <span class="card-title">{{ task.day }}</span>
        {{ task.text }}
      </div>
      <div class="card-action">
        <a href="#">Test-Remove</a>
        <i class="material-icons">add_alert</i>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: {
    task: Object,
    reminder: Boolean,
  },
};
</script>
