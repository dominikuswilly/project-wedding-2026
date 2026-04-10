<script setup>
import { onMounted } from 'vue';
import HeroSection from './components/HeroSection.vue'
import EventSchedule from './components/EventSchedule.vue'
import GallerySection from './components/GallerySection.vue'
import GiftSection from './components/GiftSection.vue'
import RsvpSection from './components/RsvpSection.vue'
import AudioPlayer from './components/AudioPlayer.vue'
import BottomNav from './components/BottomNav.vue'
import CoverPage from './components/CoverPage.vue'

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('is-visible');
      }
    });
  }, { threshold: 0.15 });

  document.querySelectorAll('section').forEach(section => {
    observer.observe(section);
  });
});
</script>

<template>
  <main class="app-container">
    <CoverPage />
    <HeroSection />
    <div class="content-wrapper">
      <EventSchedule />
      <GallerySection />
      <GiftSection />
      <RsvpSection />
    </div>
    <AudioPlayer />
  </main>
</template>

<style scoped>
.app-container {
  display: flex;
  flex-direction: column;
  background-color: var(--color-bg);
}

.content-wrapper {
  background-color: var(--color-secondary);
}
</style>
