<template>
  <div class="navbar" id="nav">
    <router-link to="/" class="logo">
      <img :src="logo" :alt="alt" />
    </router-link>
    <router-link to="/">Home</router-link>
    <router-link to="/pedidos">Pedidos</router-link>
  </div>
</template>

<script>
export default {
  name: "Navbar",
  props: ["logo", "alt"]
};
</script>

<style scoped>
.navbar {
  background: #222;
  border-bottom: 4px solid #111;
  padding: 15px 50px;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}

.navbar a {
  color: #fcba03;
  text-decoration: none;
  margin: 12px;
  transition: 0.5s;
}

.navbar a:hover {
  color: #fff;
}

.navbar .logo {
  margin: auto;
  margin-left: 0;
}

.logo img {
  width: 40px;
  height: 40px;
}
</style>
