<script setup>
import { ChevronUp } from 'lucide-vue-next';

defineProps({
  target: {
    type: String,
    required: true
  }
});

const scrollToTarget = (targetId) => {
  const el = document.getElementById(targetId);
  if (el) {
    el.scrollIntoView({ behavior: 'smooth' });
  }
};
</script>

<template>
  <div class="prev-btn-container">
    <button @click="scrollToTarget(target)" class="prev-btn" aria-label="Previous Section">
      <ChevronUp :size="24" :stroke-width="2.5" />
    </button>
  </div>
</template>

<style scoped>
.prev-btn-container {
  display: flex;
  justify-content: center;
  margin-bottom: 2rem;
  margin-top: -1.5rem; /* Pulled slightly upwards into the section padding */
}

.prev-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 3rem;
  height: 3rem;
  border-radius: 50%;
  background-color: var(--color-white);
  color: var(--color-primary-dark);
  box-shadow: 0 2px 8px rgba(0,0,0,0.06);
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  -webkit-tap-highlight-color: transparent;
  border: 1px solid rgba(0, 0, 0, 0.05);
}

.prev-btn:hover {
  transform: translateY(-3px);
  background-color: var(--color-secondary);
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}
</style>
