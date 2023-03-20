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
<style lang="scss">
ul {
  list-style: none;
  display: flex;
  align-items: center;
  padding: 0;
  margin: 0;
}
</style>
