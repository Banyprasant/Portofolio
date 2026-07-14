<script setup>
import { ref } from 'vue'
import HeroSection from './components/HeroSection.vue'
import AboutSection from './components/AboutSection.vue'
import ExperienceSection from './components/ExperienceSection.vue'
import SocialSection from './components/SocialSection.vue'
import ContactSection from './components/ContactSection.vue'

const navOpen = ref(false)
const navLinks = [
  { href: '#hero', label: 'Home' },
  { href: '#about', label: 'About' },
  { href: '#pengalaman', label: 'Pengalaman' },
  { href: '#social', label: 'Sosial' },
  { href: '#contact', label: 'Kontak' },
]

function closeNav() {
  navOpen.value = false
}
</script>

<template>
  <div class="app-shell">
    <!-- ============ NAV — slim HUD bar, jadi jangkar antar-section ============ -->
    <header class="sv-nav">
      <a href="#hero" class="sv-nav__brand" data-text="ALBANY" @click="closeNav">ALBANY</a>

      <button
        class="sv-nav__toggle"
        :class="{ 'is-open': navOpen }"
        aria-label="Buka menu navigasi"
        :aria-expanded="navOpen"
        @click="navOpen = !navOpen"
      >
        <span></span><span></span><span></span>
      </button>

      <nav class="sv-nav__links" :class="{ 'is-open': navOpen }">
        <a
          v-for="link in navLinks"
          :key="link.href"
          :href="link.href"
          @click="closeNav"
        >{{ link.label }}</a>
      </nav>
    </header>

    <main>
      <HeroSection id="hero" />
      <AboutSection id="about" />
      <ExperienceSection id="pengalaman" />
      <SocialSection id="social" />
      <ContactSection id="contact" />
    </main>

    <footer class="sv-footer">
      <p class="sv-eyebrow">© {{ new Date().getFullYear() }} Albany — Hak Cipta Dilindungi</p>
    </footer>
  </div>
</template>

<style scoped>
.app-shell {
  overflow-x: hidden;
}

/* ============ NAV ============ */
.sv-nav {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.9rem clamp(1.2rem, 4vw, 3rem);
  background: rgba(12, 12, 14, 0.75);
  backdrop-filter: blur(8px);
  border-bottom: 1px solid rgba(244, 244, 242, 0.08);
}

.sv-nav__brand {
  font-family: var(--font-display);
  font-size: 1.4rem;
  letter-spacing: 2px;
  color: var(--sv-white);
  text-decoration: none;
  text-shadow: 2px 0 var(--sv-red), -2px 0 var(--sv-cyan);
}

.sv-nav__links {
  display: flex;
  gap: clamp(1rem, 2vw, 2rem);
}

.sv-nav__links a {
  font-family: var(--font-mono);
  font-size: 0.85rem;
  letter-spacing: 1px;
  text-transform: uppercase;
  text-decoration: none;
  color: var(--sv-white);
  position: relative;
  padding-bottom: 3px;
}

.sv-nav__links a::after {
  content: '';
  position: absolute;
  left: 0;
  bottom: 0;
  width: 0;
  height: 2px;
  background: var(--sv-red);
  transition: width 0.25s ease;
}

.sv-nav__links a:hover::after {
  width: 100%;
}

.sv-nav__toggle {
  display: none;
  flex-direction: column;
  justify-content: center;
  gap: 5px;
  width: 34px;
  height: 34px;
  background: transparent;
  border: 1px solid rgba(244, 244, 242, 0.3);
  cursor: pointer;
}

.sv-nav__toggle span {
  display: block;
  height: 2px;
  background: var(--sv-white);
  margin: 0 6px;
  transition: transform 0.2s ease, opacity 0.2s ease;
}

.sv-nav__toggle.is-open span:nth-child(1) {
  transform: translateY(7px) rotate(45deg);
}
.sv-nav__toggle.is-open span:nth-child(2) {
  opacity: 0;
}
.sv-nav__toggle.is-open span:nth-child(3) {
  transform: translateY(-7px) rotate(-45deg);
}

/* ============ FOOTER ============ */
.sv-footer {
  text-align: center;
  padding: var(--space-md) var(--space-sm);
  border-top: 1px solid rgba(244, 244, 242, 0.08);
}

/* ============ RESPONSIVE (mobile <= 768px) ============ */
@media (max-width: 768px) {
  .sv-nav__toggle {
    display: flex;
  }

  .sv-nav__links {
    position: absolute;
    top: 100%;
    left: 0;
    right: 0;
    flex-direction: column;
    gap: 0;
    background: var(--sv-bg-panel);
    border-bottom: 3px solid var(--sv-red);
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.3s ease;
  }

  .sv-nav__links.is-open {
    max-height: 300px;
  }

  .sv-nav__links a {
    padding: 1rem 1.5rem;
    border-bottom: 1px solid rgba(244, 244, 242, 0.06);
  }
}
</style>
