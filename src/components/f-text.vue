<template>
  <div>
    <div
      class="form-group"
      v-bind:class="{ error: username.isError, success: username.isSuccess }"
    >
      <label for="username">Username</label>
      <input
        type="text"
        v-model="username.value"
        placeholder="Enter Username"
        @input="onchangeUsername"
      />
      <small v-if="username.isError">{{ username.message }}</small>
    </div>
    <div
      class="form-group"
      v-bind:class="{ error: password.isError, success: password.isSuccess }"
    >
      <label for="password">Password</label>
      <input
        type="text"
        v-model="password.value"
        placeholder="Enter Password"
        @input="onchangePassword"
      />
      <small v-if="password.isError">{{ password.message }}</small>
    </div>
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
const validateUserName = (username) => {
  isEmpty(username, "UserName");
};
const validatePassword = (password) => {
  let regex = new RegExp(
    "(?=.*[A-Za-z])(?=.*[0-9])(?=.*[^A-Za-z0-9])(?=.{8,})"
  );
  isEmpty(password, "Password");
  if (!isEmpty(password, "Password") && !regex.test(password.value)) {
    password.isError = true;
    password.isSuccess = false;
    password.message = `Minimum eight characters, at least one letter, one number and one special character`;
  }
  if (regex.test(password.value)) {
    password.isError = false;
    password.isSuccess = true;
  }
};
export default {
  name: "FText",

  data() {
    return {
      username: {
        value: "",
        message: "error",
        isError: false,
        isSuccess: false,
      },
      password: {
        value: "",
        message: "error",
        isError: false,
        isSuccess: false,
      },
    };
  },
  methods: {
    onchangeUsername() {
      validateUserName(this.username);
    },
    onchangePassword(e) {
      validatePassword(this.password);
    },
  },
};
</script>
