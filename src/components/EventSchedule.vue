<script setup>
import { MapPin, Clock, CalendarDays } from 'lucide-vue-next';
</script>

<template>
  <section id="schedule" class="schedule-section">
    <h2 class="section-title">Schedule</h2>
    <p class="text-center text-muted mb-8">Dengan memohon rahmat dan ridho Tuhan Yang Maha Esa, kami mengundang Bapak/Ibu/Saudara/i untuk menghadiri acara pernikahan kami.</p>
    
    <div class="event-card">
      <div class="event-badge">Akad / Pemberkatan</div>
      <h3 class="event-title">Gereja / Masjid XYZ</h3>
      
      <div class="event-detail">
        <CalendarDays class="icon" :size="20" />
        <span>Sabtu, 14 Februari 2026</span>
      </div>
      
      <div class="event-detail">
        <Clock class="icon" :size="20" />
        <span>09.00 - 11.00 WIB</span>
      </div>
      
      <div class="event-detail">
        <MapPin class="icon" :size="20" />
        <span>Jl. Contoh Alamat No. 123, Jakarta Selatan</span>
      </div>
      
      <a href="https://maps.app.goo.gl/dummy" target="_blank" class="btn-outline mt-4 w-full">
        <MapPin :size="18" /> Buka Google Maps
      </a>
    </div>

    <div class="event-card mt-8">
      <div class="event-badge bg-accent">Resepsi Pernikahan</div>
      <h3 class="event-title">Hotel Grand Royale Ballroom</h3>
      
      <div class="event-detail">
        <CalendarDays class="icon" :size="20" />
        <span>Sabtu, 14 Februari 2026</span>
      </div>
      
      <div class="event-detail">
        <Clock class="icon" :size="20" />
        <span>18.30 - 21.30 WIB</span>
      </div>
      
      <div class="event-detail">
        <MapPin class="icon" :size="20" />
        <span>Jl. Jendral Sudirman Kav. 45, Jakarta Pusat</span>
      </div>
      
      <a href="https://maps.app.goo.gl/dummy" target="_blank" class="btn-primary mt-4 w-full">
        <MapPin :size="18" /> Buka Google Maps
      </a>
    </div>
  </section>
</template>

<style scoped>
.schedule-section {
  background-color: var(--color-bg);
}

.event-card {
  background-color: var(--color-white);
  border-radius: 1rem;
  padding: 2rem 1.5rem;
  box-shadow: var(--shadow-md);
  position: relative;
  overflow: hidden;
  border-top: 4px solid var(--color-primary);
}

.event-card.mt-8 {
  border-top-color: var(--color-accent);
}

.event-badge {
  display: inline-block;
  background-color: var(--color-primary);
  color: var(--color-white);
  padding: 0.25rem 1rem;
  border-radius: 9999px;
  font-size: 0.8rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

.bg-accent {
  background-color: var(--color-accent);
}

.event-title {
  font-size: 1.5rem;
  margin-bottom: 1.5rem;
  color: var(--color-text);
}

.event-detail {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
  margin-bottom: 1rem;
  color: var(--color-text-light);
}

.icon {
  color: var(--color-primary-dark);
  flex-shrink: 0;
}

.w-full {
  width: 100%;
}
</style>
