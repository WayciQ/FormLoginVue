<template>
  <div
    class="form-group"
    v-bind:class="{ error: input.isError, success: input.isSuccess }"
  >
    <label for="username">{{ label }}</label>
    <input
      :type="type"
      v-model="input.value"
      :placeholder="[`Enter ${label}`]"
      @input="onchange"
    />
    <small v-if="input.isError">{{ input.message }}</small>
  </div>
</template>
<script>
const isEmpty = (input, label) => {
  if (input.value === "") {
    input.isError = true;
    input.isSuccess = false;
    input.message = `Please enter ${label}`;
    return true;
  } else {
    input.isError = false;
    input.isSuccess = true;
    return false;
  }
};
export default {
  name: "FInput",
  props: {
    label: {
      type: String,
      defautl: "Label",
    },
    placehoder: {
      type: String,
      defautl: "Label",
    },
    type: {
      type: String,
      defautl: "text",
    },
  },
  data() {
    return {
      input: {
        value: "",
        message: "error",
        isError: false,
        isSuccess: false,
      },
    };
  },
  methods: {
    onchange() {
      if (!isEmpty(this.input, this.label)) {
        this.$emit("validation", this.input);
      }
    },
  },
};
</script>
