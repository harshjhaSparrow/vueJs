<script setup lang="ts">
import { reactive, ref } from "vue";

// Define reactive data
const message = ref("Welcome to Vue 3 with TypeScript!");
const htmlContent = ref("<strong>Important:</strong> <em>Read this</em>");
const url = ref("https://www.example.com");
const imgSrc = ref("https://via.placeholder.com/150");
const buttonDisabled = ref(false);
const number = ref(0);
const showElementBoolean = ref(true);
const inputValue = ref("");
const isLarge = ref(false); // Boolean for conditional style
const items = ref(["Apple", "Banana", "Cherry"]); // List of items for rendering
// Define a list of objects
const fruits = ref([
  { name: "Apple", color: "Red" },
  { name: "Banana", color: "Yellow" },
  { name: "Cherry", color: "Red" },
]);
// Define styles conditionally
const computedStyles: any = reactive({
  backgroundColor: "yellow",
  fontSize: isLarge.value ? "24px" : "16px",
});
// Define reactive data
const class2 = ref("highlighted"); // This should be a class name as a string
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
    <div class="classx">Biding of class</div>
    <div :class="class2">Bindg of class2</div>
    <!-- Conditional rendering with v-else-if and v-else -->
    <div v-if="number > 10">Number is greater than 10</div>
    <div v-else-if="number === 10">Number is exactly 10</div>
    <div v-else>Number is less than 10</div>
    <div v-show="showElementBoolean">This depends on v-show:booleanValue</div>

    <!-- List rendering with v-for -->
    <ul>
      <li v-for="item in items" :key="item">
        {{ item }}
      </li>
    </ul>
    <ul>
      <li v-for="(fruit, index) in fruits" :key="index">
        {{ fruit.name }} -
        <span :style="{ color: fruit.color }">{{ fruit.color }}</span>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.highlighted {
  background-color: yellow;
}
.classx {
  background-color: aqua;
}
.class2 {
  color: red; /* Fix color definition */
}
.large-text {
  font-size: 24px;
}
</style>
