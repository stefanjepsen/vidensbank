<script setup>
import {  RouterView } from 'vue-router'
import NavigationHeader from './components/NavigationHeader.vue'
</script>

<template>
  <header>
    <div class="wrapper">
      <NavigationHeader />
     <!--  <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav> -->
    </div>
  </header>

  <RouterView />
</template>

<style scoped>

</style>
