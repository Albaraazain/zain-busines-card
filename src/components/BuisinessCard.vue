<template>
  <div class="card">
    <div class="shape green"></div>
    <div class="shape orange"></div>
    <div class="shape red"></div>
    <div class="text">PORTLAND</div>
  </div>
</template>

<script setup>
// No additional logic needed for this example
</script>

<style scoped>
.card {
  width: 300px;
  height: 180px;
  background-color: #f5f5f5;
  position: relative;
  overflow: hidden;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.shape {
  position: absolute;
  width: 100px;
  height: 100px;
  transform: rotate(45deg);
}

.green {
  background-color: #4CAF50;
  top: -50px;
  left: -50px;
}

.orange {
  background-color: #FF9800;
  top: -30px;
  right: -30px;
}

.red {
  background-color: #F44336;
  bottom: -30px;
  right: -30px;
}

.text {
  position: absolute;
  bottom: 20px;
  left: 20px;
  font-family: Arial, sans-serif;
  font-size: 24px;
  font-weight: bold;
  color: #333;
}
</style>