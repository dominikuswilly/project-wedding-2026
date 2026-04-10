<script setup>
import HeroSection from './components/HeroSection.vue'
import EventSchedule from './components/EventSchedule.vue'
import GallerySection from './components/GallerySection.vue'
import GiftSection from './components/GiftSection.vue'
import RsvpSection from './components/RsvpSection.vue'
import AudioPlayer from './components/AudioPlayer.vue'
</script>

<template>
  <main class="app-container">
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
