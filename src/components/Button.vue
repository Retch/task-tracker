<template>
  <button
    @click="onClick()"
    :style="{ background: color }"
    class="waves-effect waves-light btn-small"
  >
    {{ text }}
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
