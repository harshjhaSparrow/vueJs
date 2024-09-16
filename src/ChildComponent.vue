<!-- src/components/ChildComponent.vue -->
<template>
    <div>
      <h2>Child Component</h2>
      <p>{{ providedData.message }}</p>
      <p>Count: {{ providedData.count }}</p>
    </div>
  </template>
  
  <script setup lang="ts">
  import { inject } from 'vue';
  
  // Use inject to access the provided data
  const providedData = inject('providedData');
  
  // Ensure that the data is available
  if (!providedData) {
    throw new Error('No providedData found!');
  }
  </script>
  
  <style scoped>
  /* Styles for ChildComponent.vue */
  </style>
  