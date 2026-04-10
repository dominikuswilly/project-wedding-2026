<script setup>
import { ref, onMounted } from 'vue';
import { Home, CalendarDays, Image as ImageIcon, Gift, MessageCircle } from 'lucide-vue-next';

const activeSection = ref('hero');

const navItems = [
  { id: 'hero', icon: Home, label: 'Home' },
  { id: 'schedule', icon: CalendarDays, label: 'Jadwal' },
  { id: 'gallery', icon: ImageIcon, label: 'Galeri' },
  { id: 'gift', icon: Gift, label: 'Kado' },
  { id: 'rsvp', icon: MessageCircle, label: 'RSVP' }
];

const scrollTo = (id) => {
  const el = document.getElementById(id);
  if (el) {
    el.scrollIntoView({ behavior: 'smooth' });
    activeSection.value = id;
  }
};

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      // If a section is intersecting by at least 50%, mark it as active
      if (entry.isIntersecting) {
        activeSection.value = entry.target.id;
      }
    });
  }, { threshold: 0.3 });

  navItems.forEach(item => {
    const el = document.getElementById(item.id);
    if (el) observer.observe(el);
  });
});
</script>

<template>
  <nav class="bottom-nav">
    <button 
      v-for="item in navItems" 
      :key="item.id"
      class="nav-item"
      :class="{ active: activeSection === item.id }"
      @click="scrollTo(item.id)"
      :aria-label="item.label"
    >
      <div class="icon-wrapper" :class="{ 'active': activeSection === item.id }">
        <component :is="item.icon" :size="20" :stroke-width="activeSection === item.id ? 2.5 : 2" />
      </div>
      <span class="nav-label">{{ item.label }}</span>
    </button>
  </nav>
</template>

<style scoped>
.bottom-nav {
  position: fixed;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 100%;
  max-width: 480px; 
  background-color: rgba(253, 253, 249, 0.95); /* matching --color-bg */
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  display: flex;
  align-items: center;
  justify-content: space-around;
  padding: 0.5rem 0.5rem 1.5rem 0.5rem; /* Extra padding bottom for safe area */
  box-shadow: 0 -4px 20px rgba(0, 0, 0, 0.05);
  z-index: 1000;
  border-top-left-radius: 1.5rem;
  border-top-right-radius: 1.5rem;
}

.nav-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 0.3rem;
  color: var(--color-text-light);
  padding: 0.5rem;
  flex: 1;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
  -webkit-tap-highlight-color: transparent;
}

.icon-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 32px;
  border-radius: 16px;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.nav-item.active .icon-wrapper {
  background-color: var(--color-secondary);
  color: var(--color-primary-dark);
}

.nav-item.active {
  color: var(--color-primary-dark);
}

.nav-label {
  font-size: 0.65rem;
  font-weight: 600;
  opacity: 0.8;
  transition: all 0.3s ease;
}

.nav-item.active .nav-label {
  opacity: 1;
}
</style>
