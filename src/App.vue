<template>
  <div id="app">
    <div class="avatar">
      <img src="./assets/avatar.png" alt="avatar" />
    </div>
    <div class="form">
      <div
        class="form-group"
        v-bind:class="{ error: username.isError, success: username.isSuccess }"
      >
        <label for="username">Username</label>
        <input
          type="text"
          v-model="username.value"
          placeholder="Enter Username"
          @change="onchangeUsername"
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
          @change="onchangePassword"
        />
        <small v-if="password.isError">{{ password.message }}</small>
      </div>
      <button @click="submit">Login</button>
      <div class="checkbox-group">
        <input type="checkbox" v-model="remember" />
        <label for="checkbox" @click="setRemember">Remember me</label>
      </div>
      <div class="footer-group">
        <button>Cancel</button>
        <div>Forgot <a href="#">password?</a></div>
      </div>
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
  name: "app",
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
      remember: false,
    };
  },
  methods: {
    submit() {
      validateUserName(this.username);
      validatePassword(this.password);
    },
    onchangeUsername() {
      validateUserName(this.username);
    },
    onchangePassword(e) {
      validatePassword(this.password);
    },
    setRemember() {
      this.remember = !this.remember;
    },
  },
};
</script>