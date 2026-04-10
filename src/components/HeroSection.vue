<script setup>
import NextSectionBtn from './NextSectionBtn.vue';
</script>

<template>
  <section id="hero" class="hero-container">
    <div class="hero-bg">
      <img src="/images/hero.png" alt="Kevin & Sherley Pre-wedding" class="img-bg" />
      <div class="overlay"></div>
    </div>

    <div class="hero-content">
      <p class="pre-title">THE WEDDING OF</p>
      <h1 class="title">Kevin<br /><span class="and-symbol">&</span><br />Sherley</h1>

      <div class="date-container">
        <p class="date">12 . 12 . 2026</p>
      </div>

      <p class="scroll-prompt">Scroll to open</p>
      <NextSectionBtn target="schedule" :light="true" class="hero-next" />
    </div>
  </section>
</template>

<style scoped>
.hero-container {
  height: 100vh;
  min-height: 600px;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0;
  overflow: hidden;
}

.hero-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1;
}

.img-bg {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
}

.overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(to bottom,
      rgba(0, 0, 0, 0.2) 0%,
      rgba(0, 0, 0, 0.6) 50%,
      rgba(47, 54, 46, 0.9) 100%);
}

.hero-content {
  position: relative;
  z-index: 2;
  text-align: center;
  color: var(--color-white);
  padding: 2rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-end;
  height: 100%;
  padding-bottom: 4rem;
}

.pre-title {
  font-size: 0.9rem;
  letter-spacing: 0.2em;
  margin-bottom: 1.5rem;
  font-weight: 600;
  color: var(--color-secondary);
}

.title {
  font-size: 3.5rem;
  line-height: 1.1;
  margin-bottom: 2rem;
  color: var(--color-white);
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
}

.and-symbol {
  font-family: var(--font-sans);
  font-size: 2rem;
  font-style: italic;
  color: var(--color-accent);
}

.date-container {
  border-top: 1px solid var(--color-accent);
  border-bottom: 1px solid var(--color-accent);
  padding: 0.75rem 0;
  margin-bottom: 3rem;
  width: 80%;
  max-width: 250px;
}

.date {
  font-family: var(--font-serif);
  font-size: 1.25rem;
  letter-spacing: 0.1em;
}

.scroll-prompt {
  font-size: 0.8rem;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  margin-bottom: 0.5rem;
  opacity: 0.8;
}

.hero-next {
  margin-top: 0;
  padding-bottom: 0;
}
</style>
