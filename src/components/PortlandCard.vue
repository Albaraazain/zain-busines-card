<template>
  <div class="app-container">
    <h1>Portland Card Demo</h1>
    <PortlandCard />
    <div class="controls">
      <button @click="toggleAnimation">Toggle Animation</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import PortlandCard from './components/PortlandCard.vue';

const isAnimated = ref(false);

const toggleAnimation = () => {
  isAnimated.value = !isAnimated.value;
  // You would then pass this as a prop to PortlandCard if implementing animations
};
</script>

<style scoped>
.app-container {
  padding: 20px;
  max-width: 800px;
  margin: 0 auto;
}

.controls {
  margin-top: 20px;
  text-align: center;
}

button {
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
}
</style>