<script setup lang="ts">
import { ref, computed, reactive } from "vue";

// Define reactive data
const message = ref("Welcome to Vue 3 with TypeScript!");
const htmlContent = ref("<strong>Important:</strong> <em>Read this</em>");
const url = ref("https://www.example.com");
const imgSrc = ref("https://via.placeholder.com/150");
const buttonDisabled = ref(false);
const inputValue = ref("");
const isLarge = ref(false); // Boolean for conditional style

// Define styles conditionally
const computedStyles:any = reactive({
  backgroundColor: "yellow",
  fontSize: isLarge.value ? "24px" : "16px",
});
</script>

<template>
  <div>
    <!-- Binding href attribute to a URL -->
    <a :href="url" target="_blank">Visit Example</a>

    <!-- Displaying text with v-text -->
    <p v-text="message"></p>

    <!-- Displaying HTML content with v-html -->
    <div v-html="htmlContent"></div>

    <!-- Binding src attribute to an image URL -->
    <img :src="imgSrc" alt="Placeholder Image" />

    <!-- Binding disabled attribute to a boolean -->
    <button :disabled="buttonDisabled">Submit</button>

    <!-- Binding value attribute to an input field -->
    <input v-model="inputValue" placeholder="Type something here" />

    <!-- Conditional style binding -->
    <div :style="computedStyles">This div will have conditional styles</div>
  </div>
</template>

<style scoped>
.highlighted {
  background-color: yellow;
}

.large-text {
  font-size: 24px;
}
</style>
