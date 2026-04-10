<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import backgroundMusic from '../assets/shane.mpeg';

const audioRef = ref(null);
let hasInteracted = false;
let playInterval = null;

const tryPlayAudio = () => {
  if (hasInteracted || !audioRef.value) return;
  
  const playPromise = audioRef.value.play();
  
  if (playPromise !== undefined) {
    playPromise.then(() => {
      hasInteracted = true;
      if (playInterval) clearInterval(playInterval);
      removeListeners(); 
    }).catch(e => {
      // Browsers block autoplay until interaction
    });
  }
};

const removeListeners = () => {
  document.removeEventListener('click', tryPlayAudio);
  document.removeEventListener('touchstart', tryPlayAudio);
  document.removeEventListener('touchend', tryPlayAudio);
  document.removeEventListener('touchmove', tryPlayAudio);
  document.removeEventListener('scroll', tryPlayAudio);
  document.removeEventListener('keydown', tryPlayAudio);
};

onMounted(() => {
  // Attempt to play immediately the second the page and HeroSection loads
  tryPlayAudio();

  // Actively brute-force it every 1000ms until the browser allows it (usually requires user interaction on strict devices)
  playInterval = setInterval(() => {
    if (!hasInteracted) {
      tryPlayAudio();
    }
  }, 1000);

  // Hook into all possible interactions (swipes, scrolls, etc).
  document.addEventListener('click', tryPlayAudio, { passive: true });
  document.addEventListener('touchstart', tryPlayAudio, { passive: true });
  document.addEventListener('touchend', tryPlayAudio, { passive: true });
  document.addEventListener('touchmove', tryPlayAudio, { passive: true });
  document.addEventListener('scroll', tryPlayAudio, { passive: true });
  document.addEventListener('keydown', tryPlayAudio, { passive: true });
});

onUnmounted(() => {
  if (playInterval) clearInterval(playInterval);
  removeListeners();
});
</script>

<template>
  <audio ref="audioRef" autoplay loop preload="auto" :src="backgroundMusic"></audio>
</template>

<style scoped>
</style>
