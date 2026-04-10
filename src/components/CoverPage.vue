<script setup>
import { ref, onMounted } from 'vue';
import { MailOpen } from 'lucide-vue-next';

const isOpen = ref(false);
const isHidden = ref(false);
const guestName = ref('Tamu Undangan');

const openInvitation = () => {
  isOpen.value = true;
  // Enable scrolling after animation starts
  document.body.style.overflow = '';
  
  // Hide component after animation finishes
  setTimeout(() => {
    isHidden.value = true;
  }, 1000);
};

onMounted(() => {
  // Lock scrolling when mounted
  document.body.style.overflow = 'hidden';

  // Get guest name from URL query parameter 'to'
  const params = new URLSearchParams(window.location.search);
  const name = params.get('to');
  if (name) {
    // 1. Replace '+' with space and decode the URI
    const decodedName = decodeURIComponent(name.replace(/\+/g, ' '));
    // 2. Simplify input: replace '\n', '|', or ',' followed by optional space with a real newline
    guestName.value = decodedName
      .replace(/\\n/g, '\n')
      .replace(/\|/g, '\n')
      .replace(/, /g, '\n')
      .replace(/,/g, '\n');
  }
});
</script>

<template>
  <div v-if="!isHidden" class="cover-overlay" :class="{ 'is-open': isOpen }">
    <div class="cover-bg">
      <img src="/images/hero.png" alt="Wedding Cover" class="bg-img" />
      <div class="overlay"></div>
    </div>
    
    <div class="cover-content">
      <p class="pre-title">THE WEDDING OF</p>
      <h1 class="couple-names">Kevin & Sherley</h1>
      <p class="wedding-date">12 . 12 . 2026</p>
      
      <div class="recipient-box">
        <p class="recipient-label">Kepada Bapak/Ibu/Saudara/i:</p>
        <h2 class="recipient-name">{{ guestName }}</h2>
      </div>
      
      <button @click="openInvitation" class="btn-open">
        <MailOpen :size="18" /> Buka Undangan
      </button>
    </div>
  </div>
</template>

<style scoped>
.cover-overlay {
  position: fixed;
  top: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 100%;
  max-width: 480px;
  height: 100%;
  z-index: 9999;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: transform 1s cubic-bezier(0.8, 0, 0.2, 1), opacity 0.8s ease;
  overflow: hidden;
}

.cover-overlay.is-open {
  transform: translate(-50%, -100%);
  opacity: 0;
}

.cover-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: var(--color-primary-dark);
}

.bg-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  opacity: 0.6;
}

.overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(to bottom, 
    rgba(0,0,0,0.3) 0%, 
    rgba(0,0,0,0.7) 100%
  );
}

.cover-content {
  position: relative;
  z-index: 10;
  text-align: center;
  color: white;
  padding: 2rem;
  width: 100%;
  max-width: 400px;
}

.pre-title {
  font-size: 0.8rem;
  letter-spacing: 0.3em;
  margin-bottom: 1rem;
  opacity: 0.9;
}

.couple-names {
  font-size: 3rem;
  font-family: var(--font-serif);
  margin-bottom: 1rem;
  line-height: 1.2;
}

.wedding-date {
  font-size: 1.1rem;
  letter-spacing: 0.1em;
  margin-bottom: 3rem;
  color: var(--color-secondary);
}

.recipient-box {
  margin-bottom: 3rem;
  padding: 1.5rem;
  border: 1px solid rgba(255,255,255,0.2);
  background: rgba(255,255,255,0.05);
  backdrop-filter: blur(5px);
  border-radius: 1rem;
}

.recipient-label {
  font-size: 0.85rem;
  margin-bottom: 0.5rem;
  opacity: 0.8;
}

.recipient-name {
  font-size: 1.5rem;
  font-weight: 600;
  color: white;
  line-height: 1.3;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: pre-line; /* Respect actual newline characters */
}

.btn-open {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.75rem;
  background-color: var(--color-primary);
  color: white;
  padding: 1rem 2rem;
  border-radius: 9999px;
  font-weight: 600;
  font-size: 1rem;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(0,0,0,0.2);
  cursor: pointer;
  border: none;
}

.btn-open:hover {
  transform: scale(1.05);
  background-color: var(--color-primary-dark);
}

.btn-open:active {
  transform: scale(0.95);
}
</style>
