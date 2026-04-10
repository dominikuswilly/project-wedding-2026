<script setup>
import { computed } from 'vue';

const images = [
  { id: 1, src: '/images/gallery_1.png', alt: 'Pre-wedding 1' },
  { id: 2, src: '/images/gallery_2.png', alt: 'Pre-wedding 2' },
  { id: 3, src: '/images/hero.png', alt: 'Pre-wedding 3' }
];
</script>

<template>
  <section id="gallery" class="gallery-section">
    <h2 class="section-title">Our Moments</h2>
    <p class="text-center text-muted mb-8">Setiap detik bersamamu adalah puisi yang tak pernah selesai kutulis.</p>
    
    <div class="gallery-grid">
      <div v-for="(img, idx) in images" :key="img.id" class="gallery-item" :class="'item-' + idx">
        <img :src="img.src" :alt="img.alt" loading="lazy" class="gallery-img" />
      </div>
    </div>
  </section>
</template>

<style scoped>
.gallery-section {
  background-color: var(--color-white);
}

.gallery-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1rem;
}

.gallery-item {
  border-radius: 0.5rem;
  overflow: hidden;
  box-shadow: var(--shadow-sm);
}

/* Make the first image span full width for masonry-like feel */
.item-0 {
  grid-column: span 2;
  height: 250px;
}

.item-1, .item-2 {
  height: 200px;
}

.gallery-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.gallery-img:hover {
  transform: scale(1.05);
}
</style>
