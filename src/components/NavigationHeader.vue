<template>
    <nav class="nav-header">
      <div class="nav-container">
        <RouterLink to="/" class="nav-link">Home</RouterLink>
        <RouterLink to="/about" class="nav-link">About</RouterLink>
      </div>
    </nav>
  </template>
  
  <script setup>
  import { RouterLink } from 'vue-router';
  </script>
  
  <style scoped>
  .nav-header {
    background-color: #fff;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  }
  
  .nav-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    max-width: 1200px;
    margin: 0 auto;
    padding: 10px 20px;
  }
  
  .nav-link {
    text-decoration: none;
    color: #333;
    font-weight: bold;
    padding: 10px 15px;
    border-radius: 8px;
    transition: background-color 0.2s;
  }
  
  .nav-link:hover {
    background-color: #f0f0f0;
  }
  </style>
  