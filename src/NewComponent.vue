<!-- src/components/NewComponent.vue -->
<template>
    <div class="new-component" v-bind="attrs">
      <h2>{{ title }}</h2>
      <p>{{ message }}</p>
      <button @click="handleClick">Click Me</button>
    </div>
  </template>
  
  <script setup lang="ts">
  import { defineProps, useAttrs } from 'vue';
  
  // Define props
  const props = defineProps({
    title: {
      type: String,
      default: 'Default Title',
    },
    message: {
      type: String,
      default: 'Default message',
    }
  });
  
  // Use non-prop attributes
  const attrs = useAttrs();
  
  const handleClick = () => {
    alert("Button clicked in NewComponent!");
  };
  </script>
  
  <style scoped>
  .new-component {
    background-color: #f5f5f5;
    padding: 15px;
    border: 1px solid #ccc;
  }
  </style>
  