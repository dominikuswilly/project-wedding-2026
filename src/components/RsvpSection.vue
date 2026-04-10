<script setup>
import { MessageCircle } from 'lucide-vue-next';

const waNumber = "6281234567890";
const message = "Halo Kevin & Sherley, saya [Nama Anda] ingin konfirmasi kehadiran pada acara pernikahan kalian. Terima kasih!";
const waLink = `https://wa.me/${waNumber}?text=${encodeURIComponent(message)}`;
</script>

<template>
  <section id="rsvp" class="rsvp-section">
    <div class="rsvp-card">
      <h2 class="section-title mb-4">RSVP</h2>
      <p class="text-center text-muted mb-8">
        Merupakan suatu kehormatan dan kebahagiaan bagi kami apabila Bapak/Ibu/Saudara/i berkenan hadir di acara pernikahan kami.
      </p>
      
      <a :href="waLink" target="_blank" class="btn-primary w-full">
        <MessageCircle :size="18" /> Konfirmasi Via WhatsApp
      </a>
    </div>

    <footer class="footer">
      <p class="closing">Terima Kasih</p>
      <h2 class="couple-name">Kevin & Sherley</h2>
    </footer>
  </section>
</template>

<style scoped>
.rsvp-section {
  background-color: var(--color-white);
  padding-bottom: 6rem; /* Extra space for resting scroll */
}

.rsvp-card {
  background-color: var(--color-bg);
  border-radius: 1rem;
  padding: 2.5rem 1.5rem;
  box-shadow: var(--shadow-sm);
  text-align: center;
  margin-bottom: 4rem;
}

.w-full {
  width: 100%;
}

.footer {
  text-align: center;
  padding: 1rem 0;
}

.closing {
  font-size: 0.9rem;
  text-transform: uppercase;
  letter-spacing: 0.2rem;
  color: var(--color-text-light);
  margin-bottom: 1rem;
}

.couple-name {
  font-size: 2.5rem;
  color: var(--color-primary-dark);
}
</style>
