<template>
  <button
    @click="onClick()"
    :style="{ background: color }"
    class="btn-floating btn-large waves-effect waves-light green z-depth-2 hoverable"
  >
    <i class="material-icons">{{ text }}</i>
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    text: {
      type: String,
      default: "default button",
    },
    color: {
      type: String,
    },
  },
  methods: {
    onClick() {
      this.$emit("btn-click");
    },
  },
};
</script>
