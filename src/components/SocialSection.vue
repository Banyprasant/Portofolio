<script setup>
import { ref } from 'vue'

// State reactive: menyimpan medsos mana yang lagi "aktif" (baru diklik)
const activeSocial = ref(null)

const socials = [
  {
    key: 'instagram',
    label: 'Instagram',
    href: 'https://www.instagram.com/albany.prasants/',
    position: { top: '8%', left: '12%' },
    delay: '0s',
  },
  {
    key: 'linkedin',
    label: 'LinkedIn',
    href: 'https://www.linkedin.com/in/albany-prayoga-santoso-3929743a9/',
    position: { top: '48%', left: '68%' },
    delay: '0.6s',
  },
  {
    key: 'github',
    label: 'GitHub',
    href: 'https://github.com/Banyprasant',
    position: { top: '70%', left: '28%' },
    delay: '1.1s',
  },
]

function handleClick(item) {
  activeSocial.value = item.key
}
</script>

<template>
  <section class="social">
    <div class="social__header">
      <p class="sv-eyebrow">// CONNECT.LINK</p>
      <h2 class="social__title">Ayo Terhubung</h2>
      <p class="social__hint">(Klik salah satu ikon untuk menuju akun media sosial)</p>
    </div>

    <!-- ============ KONTAINER RELATIF — ikon disebar & mengambang ============ -->
    <div class="social__field">
      <a
        v-for="item in socials"
        :key="item.key"
        :href="item.href"
        target="_blank"
        rel="noopener noreferrer"
        class="social-btn"
        :class="[item.key, { 'is-active': activeSocial === item.key }]"
        :style="{
          top: item.position.top,
          left: item.position.left,
          animationDelay: item.delay,
        }"
        :aria-label="item.label"
        @click="handleClick(item)"
      >
        <!-- Instagram: kamera sederhana -->
        <svg v-if="item.key === 'instagram'" viewBox="0 0 24 24" class="social-btn__icon">
          <rect x="3" y="3" width="18" height="18" rx="5" fill="none" stroke="currentColor" stroke-width="1.8" />
          <circle cx="12" cy="12" r="4.2" fill="none" stroke="currentColor" stroke-width="1.8" />
          <circle cx="17.2" cy="6.8" r="1.1" fill="currentColor" />
        </svg>

        <!-- LinkedIn: badge "in" -->
        <svg v-else-if="item.key === 'linkedin'" viewBox="0 0 24 24" class="social-btn__icon">
          <rect x="3" y="3" width="18" height="18" rx="3" fill="none" stroke="currentColor" stroke-width="1.8" />
          <text x="6.5" y="16.5" font-size="10" font-family="var(--font-body)" font-weight="700" fill="currentColor">in</text>
        </svg>

        <!-- GitHub: ikon kode sederhana -->
        <svg v-else viewBox="0 0 24 24" class="social-btn__icon">
          <circle cx="12" cy="12" r="9" fill="none" stroke="currentColor" stroke-width="1.8" />
          <path d="M9 8.5 6 12l3 3.5M15 8.5 18 12l-3 3.5" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" />
        </svg>

        <span class="social-btn__label">{{ item.label }}</span>
      </a>
    </div>
  </section>
</template>

<style scoped>
.social {
  padding: var(--space-xl) clamp(1.2rem, 4vw, 3rem);
  background: var(--sv-bg);
}

.social__header {
  max-width: var(--section-max-width);
  margin: 0 auto;
  text-align: center;
}

.social__title {
  font-size: clamp(1.8rem, 3.5vw, 2.6rem);
  margin: 0.5rem 0 0.3rem;
}

.social__hint {
  font-family: var(--font-mono);
  font-size: 0.85rem;
  color: rgba(244, 244, 242, 0.5);
}

/* ============ FIELD RELATIF — tempat ikon "mengambang" ============ */
.social__field {
  position: relative;
  max-width: var(--section-max-width);
  margin: var(--space-lg) auto 0;
  height: 320px;
}

.social-btn {
  position: absolute;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.4rem;
  width: 78px;
  text-decoration: none;
  color: rgba(244, 244, 242, 0.65);

  /* Animasi mengambang naik-turun, lihat @keyframes float di bawah */
  animation: float 4.5s ease-in-out infinite;
}

.social-btn__icon {
  width: 56px;
  height: 56px;
  padding: 14px;
  border-radius: 50%;
  border: 2px solid currentColor;
  background: var(--sv-bg-panel);
  transition: transform 0.3s cubic-bezier(0.34, 1.56, 0.64, 1), background 0.3s ease, color 0.3s ease, border-color 0.3s ease;
}

.social-btn__label {
  font-family: var(--font-mono);
  font-size: 0.7rem;
  letter-spacing: 1px;
  text-transform: uppercase;
}

@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-15px); }
}

/* ============ WARNA ASLI SAAT AKTIF (diklik) ============ */
.social-btn.instagram.is-active .social-btn__icon {
  color: #fff;
  border-color: transparent;
  background: linear-gradient(45deg, #f58529, #dd2a7b, #8134af);
  transform: scale(1.2);
}

.social-btn.linkedin.is-active .social-btn__icon {
  color: #fff;
  border-color: #0077b5;
  background: #0077b5;
  transform: scale(1.2);
}

.social-btn.github.is-active .social-btn__icon {
  color: #fff;
  border-color: #333;
  background: #333;
  transform: scale(1.2);
}

.social-btn.is-active .social-btn__label {
  color: var(--sv-white);
}

/* ============ RESPONSIVE (mobile <= 768px) ============ */
@media (max-width: 768px) {
  .social__field {
    height: auto;
    display: flex;
    justify-content: center;
    gap: var(--space-lg);
  }

  .social-btn {
    position: static;
    animation: none;
  }
}
</style>
