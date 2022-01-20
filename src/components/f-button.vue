<template>
  <button @click="submit">Login</button>
</template>
<script>
export default {
  name: "FButton",
  props: ["username", "password"],
  methods: {
    submit() {
      this.$emit("submit");
    },
  },
};
</script>
