<template>
    <nav class="nav-header">
      <div class="nav-container">
        <RouterLink to="/" class="nav-link">Vis info</RouterLink>
        <RouterLink to="/about" class="nav-link">Opret info</RouterLink>
        <button class="logout-button" @click="refreshPage">log Ud</button>
      </div>
    </nav>
  </template>
  
  <script setup>
  import { RouterLink } from 'vue-router';
  
  

  </script>


<script>
export default {
  methods: {
    refreshPage() {
      // Reload the page
      window.location.reload();
    }
  }
};
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

  .logout-button {
  padding: 10px 20px;
  background-color: #ff6666; /* Red button color */
  color: #fff; /* White text color */
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
  transition: background-color 0.2s;
}

.logout-button:hover {
  background-color: #ff3333; /* Darker red button color on hover */
}
  </style>
  