<script setup>
import { ref, onMounted } from 'vue';
import { Volume2, VolumeX } from 'lucide-vue-next';

const isPlaying = ref(false);
const audioRef = ref(null);
const hidePrompt = ref(false);

const toggleAudio = () => {
  if (!audioRef.value) return;
  hidePrompt.value = true;
  
  if (isPlaying.value) {
    audioRef.value.pause();
    isPlaying.value = false;
  } else {
    audioRef.value.play().then(() => {
      isPlaying.value = true;
    }).catch(e => {
      console.log('Autoplay prevented', e);
    });
  }
};

onMounted(() => {
  // Adding global scroll listener to remove the prompt text when they scroll
  window.addEventListener('scroll', () => {
    if (window.scrollY > 100) hidePrompt.value = true;
  }, { once: true });
});
</script>

<template>
  <div class="audio-control-container">
    <div class="audio-prompt" :class="{ 'hidden': hidePrompt }">
      Tap to play music
    </div>
    <button @click="toggleAudio" class="audio-toggle-btn" aria-label="Toggle Music">
      <Volume2 v-if="isPlaying" :size="24" />
      <VolumeX v-else :size="24" />
    </button>
    <audio ref="audioRef" loop>
      <!-- Dummy audio source -->
      <source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" type="audio/mpeg" />
    </audio>
  </div>
</template>

<style scoped>
.audio-control-container {
  position: fixed;
  bottom: 2rem;
  right: 1.5rem;
  z-index: 1000;
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.audio-prompt {
  background-color: var(--color-primary-dark);
  color: white;
  padding: 0.35rem 0.75rem;
  border-radius: 1rem;
  font-size: 0.75rem;
  font-weight: 500;
  box-shadow: var(--shadow-sm);
  transition: opacity 0.5s ease;
  animation: pulse 2s infinite;
}

.audio-prompt.hidden {
  opacity: 0;
  pointer-events: none;
}

.audio-toggle-btn {
  background-color: var(--color-primary);
  color: white;
  width: 48px;
  height: 48px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: var(--shadow-md);
  transition: all 0.3s ease;
}

.audio-toggle-btn:hover {
  transform: scale(1.05);
  background-color: var(--color-primary-dark);
}

@keyframes pulse {
  0% { transform: scale(1); }
  50% { transform: scale(1.05); }
  100% { transform: scale(1); }
}
</style>
