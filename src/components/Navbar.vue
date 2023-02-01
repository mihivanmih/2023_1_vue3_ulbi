<template>
  <div class="navbar">
    <router-link to="/">Главная</router-link>
    <router-link to="/posts">Посты</router-link>
    <router-link to="/about">О сайте</router-link>
    <router-link to="/store">Store</router-link>
    <router-link to="/api">Api</router-link>
    <router-link to="/echarts">Echarts</router-link>
  </div>
</template>

<script>
export default {
  name: "Navbar"
}
</script>

<style scoped>
  .navbar {
    height: 50px;
    background: teal;
    box-shadow: 2px 2px 4px gray;
    display: flex;
  }

  .navbar a {
    padding: 0 10px;
    color: #fff;
    line-height: 50px;
  }
  .navbar .router-link-active {
    color: #d54747;
  }
</style>