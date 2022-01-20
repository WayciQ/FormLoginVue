<template>
  <div class="avatar">
    <img :src="image" alt="avatar" />
  </div>
</template>

<script>
import image from "../assets/avatar.png";
export default {
  name: "FImage",
  data() {
    return {
      image: image,
    };
  },
};
</script>i