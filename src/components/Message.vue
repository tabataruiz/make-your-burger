<template>
  <div class="message-container">
    <p>{{ msg }}</p>
  </div>
</template>

<script>
export default {
  name: "Message",
  props: {
    msg: String
  }
};
</script>

<style scoped>
.message-container {
  color: #00000090;
  background: #c4f6da;
  border-left: 5px solid #3bc27a;
  padding: 10px;
  border-radius: 5px;
  max-width: 400px;
  margin: 0 auto 30px;
}

.message-container p {
  margin-bottom: 0;
}
</style>
