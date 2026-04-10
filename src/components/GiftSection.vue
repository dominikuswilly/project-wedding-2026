<script setup>
import { ref } from 'vue';
import { Copy, Check, QrCode } from 'lucide-vue-next';

const isCopiedBCA = ref(false);
const isCopiedMandiri = ref(false);

const copyToClipboard = async (text, type) => {
  try {
    await navigator.clipboard.writeText(text);
    if (type === 'BCA') {
      isCopiedBCA.value = true;
      setTimeout(() => isCopiedBCA.value = false, 2000);
    } else {
      isCopiedMandiri.value = true;
      setTimeout(() => isCopiedMandiri.value = false, 2000);
    }
  } catch (err) {
    console.error('Failed to copy', err);
  }
};
</script>

<template>
  <section id="gift" class="gift-section">
    <h2 class="section-title">Wedding Gift</h2>
    <p class="text-center text-muted mb-8">
      Doa restu Anda merupakan karunia yang sangat berarti bagi kami. 
      Jika Anda ingin memberikan tanda kasih untuk kami, dapat melalui:
    </p>

    <!-- Bank Cards -->
    <div class="bank-card">
      <div class="bank-header">
        <h3 class="bank-name">BCA</h3>
      </div>
      <p class="account-number">1234 5678 90</p>
      <p class="account-name">a.n. Kevin Richardson Bunawan</p>
      
      <button @click="copyToClipboard('1234567890', 'BCA')" class="btn-copy">
        <Check v-if="isCopiedBCA" :size="16" />
        <Copy v-else :size="16" />
        {{ isCopiedBCA ? 'Tersalin!' : 'Salin Rekening' }}
      </button>
    </div>

    <div class="bank-card">
      <div class="bank-header">
        <h3 class="bank-name">Mandiri</h3>
      </div>
      <p class="account-number">0987 6543 21</p>
      <p class="account-name">a.n. Sherley</p>
      
      <button @click="copyToClipboard('0987654321', 'Mandiri')" class="btn-copy">
        <Check v-if="isCopiedMandiri" :size="16" />
        <Copy v-else :size="16" />
        {{ isCopiedMandiri ? 'Tersalin!' : 'Salin Rekening' }}
      </button>
    </div>

    <!-- QRIS Card -->
    <div class="bank-card qris-card">
      <div class="bank-header justify-center">
        <QrCode class="icon" />
        <h3 class="bank-name">QRIS Payment</h3>
      </div>
      
      <div class="qris-placeholder">
        <div class="qris-box">
          <div class="qris-inner">QRIS<br/>DUMMY</div>
        </div>
      </div>
      <p class="account-name text-center mt-4">Kevin & Sherley</p>
    </div>

  </section>
</template>

<style scoped>
.gift-section {
  background-color: var(--color-bg);
}

.bank-card {
  background-color: var(--color-white);
  border-radius: 1rem;
  padding: 1.5rem;
  margin-bottom: 1.5rem;
  box-shadow: var(--shadow-sm);
  border: 1px solid var(--color-secondary);
  text-align: center;
}

.bank-header {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

.bank-name {
  font-family: var(--font-sans);
  font-weight: 700;
  font-size: 1.25rem;
  color: #005A9C; /* Bank generic color */
}

.account-number {
  font-size: 1.5rem;
  font-family: monospace;
  font-weight: 600;
  letter-spacing: 2px;
  color: var(--color-text);
  margin-bottom: 0.25rem;
}

.account-name {
  color: var(--color-text-light);
  font-size: 0.9rem;
  margin-bottom: 1.5rem;
}

.btn-copy {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  background-color: var(--color-secondary);
  color: var(--color-primary-dark);
  padding: 0.5rem 1rem;
  border-radius: 9999px;
  font-weight: 600;
  font-size: 0.85rem;
  transition: background-color 0.2s;
  width: 100%;
}

.btn-copy:hover {
  background-color: #dce3d4;
}

.qris-card {
  background-color: #fdfdfd;
}

.qris-placeholder {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #fff;
  padding: 1rem;
  border-radius: 0.5rem;
  border: 2px dashed #ccc;
  width: 200px;
  height: 200px;
  margin: 0 auto;
}

.qris-box {
  width: 100%;
  height: 100%;
  background: repeating-linear-gradient(
    45deg,
    #000,
    #000 10px,
    #fff 10px,
    #fff 20px
  );
  display: flex;
  justify-content: center;
  align-items: center;
}

.qris-inner {
  background-color: #fff;
  padding: 1rem;
  font-weight: bold;
  text-align: center;
}
</style>
