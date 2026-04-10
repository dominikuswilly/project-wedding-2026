<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

// Target set to 12 Dec 2026 09:00 WIB (UTC+7)
const targetDate = new Date('2026-12-12T09:00:00+07:00').getTime();

const days = ref(0);
const hours = ref(0);
const minutes = ref(0);
const seconds = ref(0);

let timer = null;

const calculateTimeLeft = () => {
  const now = new Date().getTime();
  const difference = targetDate - now;

  if (difference > 0) {
    days.value = Math.floor(difference / (1000 * 60 * 60 * 24));
    hours.value = Math.floor((difference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
    minutes.value = Math.floor((difference % (1000 * 60 * 60)) / (1000 * 60));
    seconds.value = Math.floor((difference % (1000 * 60)) / 1000);
  } else {
    days.value = 0;
    hours.value = 0;
    minutes.value = 0;
    seconds.value = 0;
    if (timer) clearInterval(timer);
  }
};

onMounted(() => {
  calculateTimeLeft();
  timer = setInterval(calculateTimeLeft, 1000);
});

onUnmounted(() => {
  if (timer) clearInterval(timer);
});
</script>

<template>
  <div class="countdown-container">
    <div class="time-box">
      <span class="number">{{ days }}</span>
      <span class="label">Days</span>
    </div>
    <div class="time-box">
      <span class="number">{{ hours }}</span>
      <span class="label">Hours</span>
    </div>
    <div class="time-box">
      <span class="number">{{ minutes }}</span>
      <span class="label">Minutes</span>
    </div>
    <div class="time-box">
      <span class="number">{{ seconds }}</span>
      <span class="label">Seconds</span>
    </div>
  </div>
</template>

<style scoped>
.countdown-container {
  display: flex;
  gap: 0.8rem;
  justify-content: center;
  margin-bottom: 2rem;
}

.time-box {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: rgba(47, 54, 46, 0.4); /* subtly dark transparent */
  padding: 0.6rem 0.6rem;
  border-radius: 0.5rem;
  min-width: 65px;
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
  border: 1px solid rgba(255, 255, 255, 0.15);
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}

.number {
  font-family: var(--font-serif);
  font-size: 1.6rem;
  font-weight: 500;
  color: var(--color-white);
  line-height: 1.1;
  text-shadow: 0 2px 4px rgba(0,0,0,0.3);
  margin-bottom: 0.1rem;
}

.label {
  font-family: var(--font-sans);
  font-size: 0.65rem;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: var(--color-secondary);
  font-weight: 600;
}
</style>
