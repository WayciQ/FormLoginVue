<template>
  <div class="checkbox-group">
    <input type="checkbox" v-model="remember" />
    <label for="checkbox" @click="setRemember">Remember me</label>
  </div>
</template>

<script>
export default {
  name: "fCheckbox",
  data() {
    return {
      remember: false,
    };
  },
  methods: {
    setRemember() {
      this.remember = !this.remember;
    },
  },
};
</script>