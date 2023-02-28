<template>
  <div class="message">
    <h1>{{ message }}</h1>
  </div>
</template>

<script>
export default {
  name: "message",
  props: {
    message: {
      type: String,
      required: true,
    },
  },
}
</script>

<style scoped>
.message {
  text-align: center;
  padding: 20px;
}
h1 {
  color: red;
}
</style>
