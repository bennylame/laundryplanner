<script setup>
import { RouterLink } from 'vue-router'
</script>
<template>
  <header>
    <nav class="container">
      <div class="branding">
        <img src="../assets/Vue_Logo_Black.png" alt="Vue logo" />
        <h1>Vue Todos</h1>
      </div>
      <ul class="nav-routes">
        <li><RouterLink to="/">Home</RouterLink></li>
        <li><RouterLink to="/about">About</RouterLink></li>
      </ul>
    </nav>
  </header>
</template>
<style lang="scss" scoped>
header {
  background-color: #f5f5f5;

  nav {
    display: flex;
    align-items: center;
    padding: 25px 16px;

    .branding {
      display: flex;
      align-items: center;
      gap: 8px;
      img {
        max-width: 50px;
      }

      h1 {
        font-size: 24px;
      }
    }

    .nav-routes {
      display: flex;
      gap: 16px;
      list-style: none;
      flex: 1;
      justify-content: flex-end;
    }

    a {
      text-decoration: none;
      color: inherit;
    }
  }
}
</style>
