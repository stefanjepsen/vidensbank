<template>
  <div class="about-view">
    <h1>About Us</h1>
    <p>Welcome to our About Us page! Here you can find information about our team.</p>
    <FormComponent />
  </div>
</template>

<script setup>
import FormComponent from "@/components/FormComponent.vue"; // Update the path as per your project structure
</script>

<style scoped>
.about-view {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}
</style>
