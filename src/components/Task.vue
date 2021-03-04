<template>
  <div class="col s12">
    <div class="card blue-grey darken-1">
      <div class="card-content white-text">
        <span class="card-title">{{ task.day }}</span>
        {{ task.text }}
        {{ task.reminder }}
      </div>
      <div class="card-action">
        <a @click="$emit('delete-task', task.id)">Test-Remove</a>
        <i @click="$emit('toggle-reminder', task.id)" class="material-icons">add_alert</i>
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
