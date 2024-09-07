<template>
  <div class="card-container" :class="{ 'ar': isArabic }">
    <div class="background-decoration"></div>

    <div class="language-toggle glassmorphism">
      <button @click="toggleLanguage('en')" :class="{ 'active': !isArabic }">EN</button>
      <button @click="toggleLanguage('ar')" :class="{ 'active': isArabic }">عربي</button>
    </div>

    <div class="logo-container">
      <img src="../assets/saqr_alshamal_logo.svg" alt="Brand Logo 1" class="brand-svg left-logo">
      <img src="../assets/florya_logo.svg" alt="Brand Logo 2" class="brand-svg right-logo">
    </div>

    <div class="card glassmorphism" ref="card" :style="cardStyle" @mousemove="handleMouseMove" @mouseleave="handleMouseLeave">
      <div class="card-content" :style="contentStyle">
        <div class="card-face card-front">
          <div class="left-section">
            <div class="logo" ref="logo">
              <span class="paw-print">🐾</span>
            </div>
            <h1 class="company-name">SANABEL AL-ANDALUS</h1>
          </div>
          <div class="right-section">
            <div class="personal-info">
              <p class="name">DR. TAHER MOHAMED ZEIN</p>
              <p class="title">TECHNICAL DIRECTOR</p>
            </div>
            <div class="contact-info">
              <p v-for="(item, index) in contactItemsEn" :key="index"
                 :class="item.type"
                 @mouseenter="highlightContact(item.type)"
                 @mouseleave="resetHighlight">
                <span class="icon">{{ item.icon }}</span> {{ item.text }}
              </p>
            </div>
          </div>
        </div>
        <div class="card-face card-back">
          <div class="right-section">
            <div class="logo" ref="logoAr">
              <span class="paw-print">🐾</span>
            </div>
            <h1 class="company-name">سنابل الأندلس</h1>
          </div>
          <div class="left-section">
            <div class="personal-info">
              <p class="name">د. طاهر محمد زين</p>
              <p class="title">المدير الفني</p>
            </div>
            <div class="contact-info">
              <p v-for="(item, index) in contactItemsAr" :key="index"
                 :class="item.type"
                 @mouseenter="highlightContact(item.type)"
                 @mouseleave="resetHighlight">
                <span class="icon">{{ item.icon }}</span> {{ item.text }}
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue';

const card = ref(null);
const logo = ref(null);
const logoAr = ref(null);
const isArabic = ref(false);

const toggleLanguage = (lang) => {
  isArabic.value = lang === 'ar';
};

const handleMouseMove = (e) => {
  if (!card.value || (!logo.value && !logoAr.value)) return;
  const rect = card.value.getBoundingClientRect();
  const x = (e.clientX - rect.left) / rect.width;
  const y = (e.clientY - rect.top) / rect.height;
  const rotateY = (x - 0.5) * 10;
  const rotateX = (y - 0.5) * -10;
  card.value.style.transform = `perspective(1000px) rotateX(${rotateX}deg) rotateY(${rotateY}deg)`;
  const currentLogo = isArabic.value ? logoAr.value : logo.value;
  currentLogo.style.transform = `translate(${(x - 0.5) * 20}px, ${(y - 0.5) * 20}px)`;
};

const handleMouseLeave = () => {
  if (!card.value || (!logo.value && !logoAr.value)) return;
  card.value.style.transform = 'perspective(1000px) rotateX(0) rotateY(0)';
  logo.value.style.transform = 'translate(0, 0)';
  logoAr.value.style.transform = 'translate(0, 0)';
};

const highlightContact = (type) => {
  if (!card.value) return;
  card.value.setAttribute('data-highlight', type);
};

const resetHighlight = () => {
  if (!card.value) return;
  card.value.removeAttribute('data-highlight');
};

const contactItemsEn = [
  { icon: '✉', text: 'anas7000@gmail.com', type: 'email' },
  { icon: '☏', text: '+966 555 972 974', type: 'phone' },
  { icon: '🌐', text: 'sanabelalanduls.com', type: 'website' },
  { icon: '📍', text: 'SAUDI ARABIA, JEDDAH, AL-RAWABI DISTRICT, KM 10', type: 'address' },
];

const contactItemsAr = [
  { icon: '✉', text: 'anas7000@gmail.com', type: 'email' },
  { icon: '☏', text: '+966 555 972 974', type: 'phone' },
  { icon: '🌐', text: 'sanabelalanduls.com', type: 'website' },
  { icon: '📍', text: 'السعودية. جدة, حي الروابي - الكيلو 10', type: 'address' },
];

const cardStyle = computed(() => ({
  transform: isArabic.value ? 'rotateY(180deg)' : 'rotateY(0deg)',
}));

const contentStyle = computed(() => ({
  transform: isArabic.value ? 'rotateY(-180deg)' : 'rotateY(0deg)',
}));

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
  handleScroll();
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
});

const handleScroll = () => {
  if (card.value) {
    const rect = card.value.getBoundingClientRect();
    const scrollPercentage = Math.max(0, Math.min(1, 1 - (rect.bottom / window.innerHeight)));
    card.value.style.setProperty('--scroll', scrollPercentage.toFixed(2));
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&family=Noto+Kufi+Arabic:wght@300;400;600&display=swap');

.card-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  background-color: #f8f9fa;
  background-image: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
  padding: 20px;
  font-family: 'Poppins', sans-serif;
  color: #333;
  position: relative;
  overflow: hidden;
}

.card-container.ar {
  font-family: 'Noto Kufi Arabic', sans-serif;
}

.background-decoration {
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: radial-gradient(circle, rgba(0,0,0,0.03) 0%, rgba(0,0,0,0) 70%);
  animation: rotate 30s linear infinite;
}

@keyframes rotate {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.logo-container {
  position: absolute;
  top: 20px;
  left: 20px;
  right: 20px;
  display: flex;
  justify-content: space-between;
  z-index: 10;
}

.brand-svg {
  width: clamp(80px, 15vw, 150px);
  height: auto;
  transition: transform 0.3s ease;
}

.brand-svg:hover {
  transform: scale(1.1);
}

.language-toggle {
  position: fixed;
  top: 20px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  border-radius: 25px;
  overflow: hidden;
  z-index: 20;
}

.language-toggle button {
  padding: 10px 20px;
  border: none;
  background-color: transparent;
  cursor: pointer;
  transition: all 0.3s ease;
  font-family: inherit;
  font-size: 14px;
  color: #495057;
  font-weight: 600;
}

.language-toggle button.active {
  background-color: rgba(0, 0, 0, 0.1);
  color: #212529;
}

.glassmorphism {
  background: rgba(255, 255, 255, 0.7);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.18);
  box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.1);
}

.card {
  width: 100%;
  max-width: 700px;
  aspect-ratio: 16 / 9;
  position: relative;
  transition: transform 0.6s;
  transform-style: preserve-3d;
  border-radius: 20px;
  overflow: hidden;
  z-index: 5;
}

.card-content {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.6s;
  transform-style: preserve-3d;
}

.card-face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  display: flex;
}

.card-back {
  transform: rotateY(180deg);
}

.left-section, .right-section {
  flex: 1;
  padding: clamp(20px, 5vw, 40px);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.left-section {
  background-color: rgba(0, 0, 0, 0.03);
}

.logo {
  font-size: clamp(36px, 8vw, 48px);
  font-weight: 600;
  color: #495057;
  transition: all 0.3s ease;
}

.paw-print {
  font-size: clamp(48px, 10vw, 64px);
}

.company-name {
  font-size: clamp(20px, 4vw, 28px);
  font-weight: 600;
  margin: 15px 0;
  color: #343a40;
  text-transform: uppercase;
  letter-spacing: 2px;
  transition: all 0.3s ease;
}

.personal-info {
  margin-bottom: 15px;
}

.name {
  font-size: clamp(18px, 3.5vw, 24px);
  font-weight: 600;
  margin: 0;
  color: #343a40;
  letter-spacing: 1px;
}

.title {
  font-size: clamp(14px, 2.5vw, 18px);
  color: #6c757d;
  margin: 8px 0 0;
  font-weight: 300;
  letter-spacing: 1px;
}

.contact-info p {
  margin: 8px 0;
  display: flex;
  align-items: center;
  color: #495057;
  transition: all 0.3s ease;
  font-size: clamp(12px, 2.5vw, 16px);
  font-weight: 300;
}

.icon {
  margin-right: 12px;
  font-size: clamp(16px, 3vw, 20px);
  color: #343a40;
  transition: all 0.3s ease;
}

.card-back .icon {
  margin-right: 0;
  margin-left: 12px;
}

@media (max-width: 768px) {
  .card {
    max-width: 90%;
  }

  .left-section, .right-section {
    padding: 20px;
  }

  .contact-info {
    font-size: 14px;
  }
}

@media (max-width: 480px) {
  .card {
    aspect-ratio: auto;
    height: auto;
    min-height: 400px;
  }

  .card-face {
    flex-direction: column;
  }

  .left-section, .right-section {
    padding: 15px;
  }

  .left-section {
    flex: 0 0 auto;
  }

  .right-section {
    flex: 1 1 auto;
  }

  .company-name {
    margin: 10px 0;
  }

  .personal-info {
    margin-bottom: 10px;
  }

  .contact-info p {
    margin: 5px 0;
  }
}

.card[data-highlight="email"] .email,
.card[data-highlight="phone"] .phone,
.card[data-highlight="website"] .website,
.card[data-highlight="address"] .address {
  color: #212529;
  transform: translateX(5px);
}

.card[data-highlight="email"] .email .icon,
.card[data-highlight="phone"] .phone .icon,
.card[data-highlight="website"] .website .icon,
.card[data-highlight="address"] .address .icon {
  transform: scale(1.1);
}

@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-5px); }
}

.card {
  animation: float 6s ease-in-out infinite;
}
</style>