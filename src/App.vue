<script setup>
import {  RouterView } from 'vue-router'
import NavigationHeader from './components/NavigationHeader.vue'
import LoginForm from './components/LoginForm.vue';
</script>


<template>
  <header>
    <div class="wrapper">
      <NavigationHeader v-if="isLoggedIn" />
      <LoginForm v-else @loginSuccess="handleLoginSuccess" />
    </div>
  </header>

  <RouterView v-if="isLoggedIn" />
</template>

<script>


export default {
  data() {
    return {
      isLoggedIn: false
    };
  },
  methods: {
    handleLoginSuccess() {
      this.isLoggedIn = true; // Update the isLoggedIn status
    }
  },
  components: {
    NavigationHeader,
    LoginForm
  }
};
</script>
