<template>
  <div class="main">
    <!-- <Banner></Banner> -->
    <div class="main-container">
      <h1>Make Your Burger</h1>
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

.main-container {
  background-image: url("/public/img/burger.jpg");
  background-position: 0 -450px;
  background-size: cover;
}

h1 {
  color: #fff;
}
</style>
