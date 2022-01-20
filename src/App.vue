<template>
  <div id="app">
    <f-image></f-image>
    <div class="form">
      <f-input :label="username.label" @validation="validateUsername"></f-input>
      <f-input
        :label="password.label"
        @validation="validatePassword"
        :type="password.type"
      ></f-input>
      <f-button @submit="onSubmit"></f-button>
      <f-checkbox :label="remember.label" @isCheck="onRemember"></f-checkbox>
      <f-footer></f-footer>
    </div>
  </div>
</template>

<script>
import FImage from "./components/f-image.vue";
import FCheckbox from "./components/f-checkbox.vue";
import FFooter from "./components/f-footer.vue";
import FButton from "./components/f-button.vue";
import FInput from "./components/f-input.vue";

export default {
  components: { FImage, FCheckbox, FFooter, FButton, FInput },
  name: "app",
  data() {
    return {
      username: {
        label: "Username",
        value: "",
        isSuccess: false,
      },
      password: {
        label: "Password",
        type: "password",
        value: "",
        isSuccess: false,
      },
      remember: {
        value: false,
        label: "Remember Me",
      },
    };
  },
  methods: {
    validateUsername(username) {
      this.username.value = username.value;
      this.username.isSuccess = username.isSuccess;
    },
    validatePassword(password) {
      let regex = new RegExp(
        "(?=.*[A-Za-z])(?=.*[0-9])(?=.*[^A-Za-z0-9])(?=.{8,})"
      );
      if (!regex.test(password.value)) {
        password.isError = true;
        password.isSuccess = false;
        password.message = `Minimum eight characters, at least one letter, one number and one special character`;
      }
      if (regex.test(password.value)) {
        password.isError = false;
        password.isSuccess = true;
      }
      this.password.value = password.value;
      this.password.isSuccess = password.isSuccess;
    },
    onRemember(remember) {
      this.remember.value = remember;
    },
    onSubmit() {
      if (this.password.isSuccess && this.username.isSuccess) {
        console.log(
          "YOU ARE SUBMIT:",
          "\nUsername:",
          this.username.value,
          "\nPassword:",
          this.password.value,
          "\nRemember:",
          this.remember.value
        );
      } else {
        console.log("Please enter correct format");
      }
    },
  },
};
</script>