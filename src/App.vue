<script setup lang="ts">
import { computed, onMounted, provide, reactive, ref, watch } from "vue";
import NewComponent from "./NewComponent.vue";

// Define reactive data
const message = ref("Welcome to Vue 3 with TypeScript!");
const htmlContent = ref("<strong>Important:</strong> <em>Read this</em>");
const url = ref("https://www.example.com");
const imgSrc = ref("https://via.placeholder.com/150");
const buttonDisabled = ref(false);
const number = ref(0);
const showElementBoolean = ref(true);
const inputValue = reactive({
  name: "",
});
const isLarge = ref(false); // Boolean for conditional style

// Provide the data
provide("providedData", {
  message: "Hello from Parent!",
  count: 42,
});
// Computed styles
const computedStyles = computed(() => ({
  backgroundColor: "yellow",
  fontSize: isLarge.value ? "24px" : "16px",
}));

const count = ref(0);

// Computed property to format the count value
const formattedCount = computed(() => {
  return `The current count is ${count.value}`;
});

const class2 = ref("highlighted"); // This should be a class name as a string

// Method to increase the count
const increment = () => {
  count.value++;
};

const decrement = () => {
  count.value--;
};

// Method to reset the count
const reset = () => {
  count.value = 0;
};

// Form submission handler
const handleSubmit = (e: Event) => {
  e.preventDefault();
  console.log("Form submitted", inputValue.name);
};

// List of items for rendering
const items = ref(["Apple", "Banana", "Cherry"]);

// List of objects
const fruits = ref([
  { name: "Apple", color: "Red" },
  { name: "Banana", color: "Yellow" },
  { name: "Cherry", color: "Red" },
]);

//these are watchers ,similar to useEffect un react
watch(count, (newValue, oldValue) => {
  console.log(`Count changed from ${oldValue} to ${newValue}`);
});

watch(inputValue, (newValue) => {
  console.log(`Input value changed: ${newValue.name}`);
});

onMounted(() => {
  console.log("component is mounted successfully");
});

watch(number, (newValue, oldValue) => {
  console.log(`Number changed from ${oldValue} to ${newValue}`);
  if (newValue > 10) {
    console.log("Number is greater than 10");
  }
});

// Define the object to be provided
const providedObject = {
  message: "Hello from Parent!",
  count: 42,
};

// Use provide to make the object available to child components
provide("providedData", providedObject);
</script>

<template>
  <NewComponent
    title="Welcome to the New Component!"
    message="This is a custom message from the parent component."
    id="unique-id"
    class="custom-class"
    style="color: blue"
  />
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
    <input v-model.lazy="inputValue.name" placeholder="Type something here" />
    <button @click="handleSubmit" :disabled="buttonDisabled">Submit</button>

    <!-- Conditional style binding -->
    <div :style="computedStyles">This div will have conditional styles</div>

    <!-- Binding classes with v-bind -->
    <div class="classx">Binding of class</div>
    <div :class="class2">Binding of class2</div>

    <!-- Conditional rendering with v-if, v-else-if, and v-else -->
    <div v-if="number > 10">Number is greater than 10</div>
    <div v-else-if="number === 10">Number is exactly 10</div>
    <div v-else>Number is less than 10</div>

    <!-- Conditional rendering with v-show -->
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
  provide and inject

  <div>
    <!-- Using computed property to display formatted count -->
    <p>{{ formattedCount }}</p>
    <button @click="increment">Increment</button>
    <button @click="reset">Reset</button>
    <button @click="decrement">Decrement</button>
  </div>

  <div>
    <label for="name">Name</label>
    <form @submit.prevent="handleSubmit">
      <input type="text" v-model.number="inputValue.name" id="name" />
      <button type="submit" :disabled="buttonDisabled">Submit</button>
    </form>
  </div>

  <div id="app">
    <h1>Main Application</h1>
    <!-- Passing non-prop attributes -->
    <NewComponent
      title="Welcome to the New Component!"
      message="This is a custom message from the parent component."
      id="unique-id"
      class="custom-class"
      style="color: blue"
    />

    <!-- Child component that will consume the provided data -->
    <ChildComponent />
  </div>

  <div id="app">
    <h1>Main Application</h1>
    <ChildComponent
      title="Welcome"
      message="This is a message passed as a prop."
    />
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
