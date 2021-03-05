<template>
  <div class="row">
    <form @submit="onSubmit" class="col s12">
      <div class="row">
        <div class="input-field col s10">
          <input id="day" v-model="day" type="text" class="validate" />
          <label for="day">Day and Time</label>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s10">
          <input id="text" v-model="text" type="text" class="validate" />
          <label for="text">Text</label>
        </div>
      </div>
      <p>
        <label>
          <input v-model="reminder" type="checkbox" />
          <span>Set Reminder</span>
        </label>
      </p>
      <button
        style="background: green"
        class="btn waves-effect waves-light"
        type="submit"
        name="action"
      >
        Save Task
        <i class="material-icons right">send</i>
      </button>
    </form>
  </div>
</template>

<script>
export default {
  name: "AddTask",
  data() {
    return {
      text: "",
      day: "",
      reminder: false,
    };
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();
      if (this.text && this.day) {
        const newTask = {
          //id: Math.floor(Math.random() * 100000),
          text: this.text,
          day: this.day,
          reminder: this.reminder,
        };

        (this.text = ""), (this.day = ""), (this.reminder = false);

        this.$emit("add-task", newTask);
      }
    },
  },
};
</script>
