<template>
  <div class="about-view">
    <h1>Opret post til din vidensbank</h1>
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
