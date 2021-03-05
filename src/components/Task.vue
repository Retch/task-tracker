<template>
  <div class="col s12">
    <div class="card blue-grey darken+1 hoverable z-depth-2">
      <div class="card-content white-text">
        <span class="card-title">{{ task.day }}</span>
        {{ task.text }}
      </div>
      <div class="card-action">
        <i
          @click="$emit('delete-task', task.id)"
          style="color: white; margin-right: 15px"
          class="material-icons"
          >delete_outline</i
        >
        <i
          style="color: white"
          @click="$emit('toggle-reminder', task.id)"
          class="material-icons"
          >{{ task.reminder ? "notification_important" : "add_alert" }}</i
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: {
    task: Object,
  },
};
</script>
