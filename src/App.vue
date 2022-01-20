<template>
  <div id="app">
    <f-image></f-image>
    <div class="form">
      <f-text ref="textField"></f-text>
      <f-button></f-button>
      <f-checkbox></f-checkbox>
      <f-footer></f-footer>
    </div>
  </div>
</template>

<script>
import fImage from "./components/f-image.vue";
import FText from "./components/f-text.vue";
import FCheckbox from "./components/f-checkbox.vue";
import FFooter from "./components/f-footer.vue";
import FButton from "./components/f-button.vue";

export default {
  components: { fImage, FText, FCheckbox, FFooter, FButton },
  name: "app",
  data() {
    return {
      value: {
        username: "",
        password: "",
      },
    };
  },
  component: {
    FText,
    fImage,
    FCheckbox,
  },
};
</script>