<template>
  <div class="main">
    <Banner></Banner>
    <div class="main-container">
      <h1>Monte o seu burger</h1>
      <BurgerForm></BurgerForm>
    </div>
  </div>
</template>

<script>
import Banner from "../components/Banner.vue";
import BurgerForm from "../components/BurgerForm.vue";

export default {
  name: "Home",
  components: {
    Banner,
    BurgerForm
  }
};
</script>

<style scoped>
.main {
  background: #fafafa;
}
</style>
