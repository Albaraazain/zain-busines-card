<template>
  <div class="card-container">
    <div class="card-stack" @mousemove="handleMouseMove" @mouseleave="handleMouseLeave" ref="cardStack">
      <div class="card card-back"></div>
      <div class="card card-middle"></div>
      <div class="card card-front">
        <div class="shape shape-green"></div>
        <div class="shape shape-orange"></div>
        <div class="shape shape-red"></div>
        <div class="content">
          <div class="company-name">
            <h1>Sanabel Al-Andalus</h1>
          </div>
          <div class="contact-person">
            <p class="name">Dr. Taher Mohamed Zein</p>
            <p class="title">Technical Director</p>
          </div>
          <div class="contact-details">
            <p>anas7000@gmail.com | +966 555 972 974</p>
            <p>info@sanabelalanduls.com</p>
          </div>
          <div class="address">
            <p>Saudi Arabia, Jeddah, Al-Rawabi District, Kilometer 10</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const cardStack = ref(null);

const handleMouseMove = (e) => {
  if (!cardStack.value) return;
  const rect = cardStack.value.getBoundingClientRect();
  const x = e.clientX - rect.left;
  const y = e.clientY - rect.top;
  const centerX = rect.width / 2;
  const centerY = rect.height / 2;
  const rotateX = (y - centerY) / 20;
  const rotateY = (centerX - x) / 20;

  cardStack.value.style.transform = `perspective(1000px) rotateX(${rotateX}deg) rotateY(${rotateY}deg)`;
};

const handleMouseLeave = () => {
  if (cardStack.value) {
    cardStack.value.style.transform = 'perspective(1000px) rotateX(0) rotateY(0)';
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap');

.card-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: #f0f0f0;
  perspective: 1000px;
  font-family: 'Roboto', sans-serif;
}

.card-stack {
  position: relative;
  width: 400px;
  height: 225px;
  transition: transform 0.3s ease;
}

.card {
  position: absolute;
  width: 100%;
  height: 100%;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

.card-back {
  background-color: #e0e0e0;
  transform: translateZ(-10px) translateY(10px);
}

.card-middle {
  background-color: #e8e8e8;
  transform: translateZ(-5px) translateY(5px);
}

.card-front {
  background-color: #ffffff;
  transform: translateZ(0);
}

.shape {
  position: absolute;
  opacity: 0.1;
  transition: all 0.3s ease;
}

.shape-green {
  background-color: #4CAF50;
  width: 250px;
  height: 250px;
  bottom: -125px;
  left: -125px;
  transform: rotate(45deg);
}

.shape-orange {
  background-color: #FF9800;
  width: 200px;
  height: 200px;
  top: -100px;
  right: -100px;
  transform: rotate(45deg);
}

.shape-red {
  background-color: #F44336;
  width: 150px;
  height: 150px;
  top: -75px;
  right: 25px;
  transform: rotate(45deg);
}

.content {
  position: relative;
  z-index: 1;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 20px;
  box-sizing: border-box;
}

.company-name h1 {
  font-size: 28px;
  font-weight: 700;
  color: #333;
  margin: 0 0 10px;
}

.contact-person .name {
  font-size: 18px;
  font-weight: 700;
  color: #4CAF50;
  margin: 0;
}

.contact-person .title {
  font-size: 16px;
  color: #666;
  margin: 5px 0 0;
}

.contact-details, .address {
  font-size: 14px;
  line-height: 1.4;
  color: #333;
}

.card-stack:hover .shape-green {
  transform: rotate(60deg) scale(1.1);
}

.card-stack:hover .shape-orange {
  transform: rotate(30deg) scale(1.1);
}

.card-stack:hover .shape-red {
  transform: rotate(15deg) scale(1.1);
}

@media (max-width: 450px) {
  .card-stack {
    width: 90%;
    height: auto;
    aspect-ratio: 16 / 9;
  }

  .company-name h1 {
    font-size: 24px;
  }

  .contact-person .name {
    font-size: 16px;
  }

  .contact-person .title {
    font-size: 14px;
  }

  .contact-details, .address {
    font-size: 12px;
  }
}
</style>