<script setup>
import { ChevronDown } from 'lucide-vue-next';

defineProps({
  target: {
    type: String,
    required: true
  },
  light: {
    type: Boolean,
    default: false
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
  <div class="next-btn-container">
    <button @click="scrollToTarget(target)" class="next-btn" :class="{ 'btn-light': light }" aria-label="Next Section">
      <ChevronDown :size="28" :stroke-width="2.5" />
    </button>
  </div>
</template>

<style scoped>
.next-btn-container {
  display: flex;
  justify-content: center;
  margin-top: 3rem;
  padding-bottom: 1.5rem;
}

.next-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 3.5rem;
  height: 3.5rem;
  border-radius: 50%;
  background-color: var(--color-white);
  color: var(--color-primary-dark);
  box-shadow: 0 4px 10px rgba(0,0,0,0.08); /* subtle shadow */
  transition: all 0.3s ease;
  animation: bounce 2s infinite cubic-bezier(0.4, 0, 0.2, 1);
  -webkit-tap-highlight-color: transparent;
}

.next-btn:hover {
  transform: translateY(2px);
  background-color: var(--color-secondary);
}

.next-btn.btn-light {
  background-color: transparent;
  color: var(--color-white);
  box-shadow: none;
  border: 1px solid rgba(255,255,255,0.3);
}

@keyframes bounce {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(10px); }
}
</style>
