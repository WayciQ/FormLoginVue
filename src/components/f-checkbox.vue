<template>
  <div class="checkbox-group">
    <input type="checkbox" v-model="isCheck" />
    <label for="checkbox" @click="setCheck">{{ label }}</label>
  </div>
</template>

<script>
export default {
  name: "FCheckbox",
  props: {
    label: {
      type: String,
      default: "Label",
    },
  },
  data() {
    return {
      isCheck: false,
    };
  },
  methods: {
    setCheck() {
      this.isCheck = !this.isCheck;
      this.$emit("isCheck", this.isCheck);
    },
  },
};
</script>