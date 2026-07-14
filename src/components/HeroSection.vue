<script setup>
// Tidak butuh state khusus di Hero — murni presentasional.
// Image handling: prefer any image placed in `src/assets/` (PNG/JPG/WebP).
// If none found, falls back to `/images/FotoGW.webp` in the `public/` folder.
// To use your photo: put it in `src/assets/` (recommended) or
// `public/images/` and name it accordingly.
import { computed } from 'vue'

const heroName = 'HALO, SAYA ALBANY'
const heroRole = 'SISWA KELAS 12'

// Glob any images in src/assets — Vite will bundle them and give URLs.
// This allows the user to simply drop a file into src/assets without
// editing this component.
const assetImages = import.meta.glob('../assets/*.{png,jpg,jpeg,webp}', { eager: true, as: 'url' })
const assetUrls = Object.values(assetImages || {})

const heroPhoto = computed(() => {
  // Prefer an explicitly named file if present
  const namedKey = Object.keys(assetImages || {}).find((k) => k.endsWith('/FotoGW.webp') || k.endsWith('/foto.webp') || k.endsWith('/foto.jpg') || k.endsWith('/foto.png'))
  if (namedKey) return assetImages[namedKey]
  // otherwise use the first available asset image
  if (assetUrls.length > 0) return assetUrls[0]
  // fallback to public path (served statically). Note leading '/'
  return '/images/FotoGwGanteng.webp'
})
</script>

<template>
  <section class="hero sv-halftone">
    <div class="hero__inner">
      <div class="hero__text">
        <p class="sv-eyebrow hero__tag">// PORTFOLIO.INIT</p>

        <!-- ======================================================
             GLITCH TEXT
             ::before dan ::after mengambil isi otomatis dari
             atribut data-text, lalu diberi warna cyan & merah +
             clip-path animasi supaya terlihat "patah" (chromatic
             aberration ala Spider-Verse). Lihat <style> di bawah.
        ======================================================= -->
        <h1 class="glitch-text" :data-text="heroName">{{ heroName }}</h1>
        <h2 class="glitch-text glitch-text--sub" :data-text="heroRole">{{ heroRole }}</h2>

        <p class="hero__desc">
          Ga ganteng jadi ga punya EX😝 
        </p>

        <a href="#about" class="hero__cta">Kenalan Yuk ↓</a>
      </div>

      <div class="hero__photo-wrap">
        <!-- ======================================================
             MASKED PROFILE PHOTO
             mask-image membuat bagian bawah foto "meleleh" transparan
             sehingga menyatu dengan background gelap di belakangnya.
             Ganti src di bawah dengan foto asli kamu.
        ======================================================= -->
        <img
          class="hero__photo"
          :src="heroPhoto"
          alt="Foto profil Albany"
        />
        <div class="hero__photo-glow"></div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  padding: calc(var(--space-xl) + 2rem) clamp(1.2rem, 4vw, 3rem) var(--space-lg);
  background: radial-gradient(ellipse at 20% 20%, rgba(123, 47, 247, 0.25), transparent 55%),
              radial-gradient(ellipse at 80% 70%, rgba(21, 242, 214, 0.12), transparent 50%),
              var(--sv-bg);
}

.hero__inner {
  max-width: var(--section-max-width);
  margin: 0 auto;
  width: 100%;
  display: grid;
  grid-template-columns: 1.1fr 0.9fr;
  align-items: center;
  gap: var(--space-lg);
}

.hero__tag {
  margin-bottom: var(--space-sm);
}

/* ============ GLITCH TEXT / CHROMATIC ABERRATION ============ */
.glitch-text {
  position: relative;
  color: var(--sv-white);
  font-size: clamp(2.2rem, 5.5vw, 4rem);
  line-height: 1.05;
  z-index: 1;
}

.glitch-text--sub {
  font-size: clamp(1.4rem, 3vw, 2.2rem);
  color: var(--sv-cyan);
  margin-top: 0.4rem;
  -webkit-text-stroke: 1px var(--sv-red);
}

.glitch-text::before,
.glitch-text::after {
  content: attr(data-text);
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  z-index: -1;
  mix-blend-mode: screen;
}

.glitch-text::before {
  left: -4px;
  color: var(--sv-cyan);
  animation: glitch-anim-1 2.5s infinite linear alternate-reverse;
}

.glitch-text::after {
  left: 4px;
  color: var(--sv-red);
  animation: glitch-anim-2 3s infinite linear alternate-reverse;
}

@keyframes glitch-anim-1 {
  0% { clip-path: inset(20% 0 80% 0); transform: translate(-2px, 1px); }
  20% { clip-path: inset(60% 0 10% 0); transform: translate(2px, -1px); }
  40% { clip-path: inset(40% 0 50% 0); transform: translate(-2px, 2px); }
  60% { clip-path: inset(80% 0 5% 0); transform: translate(2px, -2px); }
  80% { clip-path: inset(10% 0 70% 0); transform: translate(-2px, 1px); }
  100% { clip-path: inset(30% 0 50% 0); transform: translate(2px, -1px); }
}

@keyframes glitch-anim-2 {
  0% { clip-path: inset(10% 0 60% 0); transform: translate(2px, 1px); }
  20% { clip-path: inset(30% 0 20% 0); transform: translate(-2px, -1px); }
  40% { clip-path: inset(70% 0 10% 0); transform: translate(2px, 2px); }
  60% { clip-path: inset(20% 0 50% 0); transform: translate(-2px, -2px); }
  80% { clip-path: inset(50% 0 30% 0); transform: translate(2px, 1px); }
  100% { clip-path: inset(5% 0 80% 0); transform: translate(-2px, -1px); }
}

.hero__desc {
  max-width: 46ch;
  margin-top: var(--space-md);
  color: rgba(244, 244, 242, 0.75);
  font-size: 1.05rem;
}

.hero__cta {
  display: inline-block;
  margin-top: var(--space-md);
  padding: 0.85rem 1.8rem;
  font-family: var(--font-mono);
  font-size: 0.9rem;
  letter-spacing: 1px;
  text-transform: uppercase;
  text-decoration: none;
  color: var(--sv-ink);
  background: var(--sv-cyan);
  clip-path: polygon(0 0, 100% 0, 96% 100%, 4% 100%);
  transition: transform 0.2s ease, background 0.2s ease;
}

.hero__cta:hover {
  background: var(--sv-red);
  color: var(--sv-white);
  transform: translateY(-3px);
}

/* ============ MASKED PROFILE PHOTO ============ */
.hero__photo-wrap {
  position: relative;
  justify-self: center;
}

.hero__photo {
  width: min(360px, 80vw);
  aspect-ratio: 4 / 5;
  object-fit: cover;
  /* Fade bawah foto menyatu ke background */
  mask-image: linear-gradient(to bottom, black 60%, transparent 100%);
  -webkit-mask-image: linear-gradient(to bottom, black 60%, transparent 100%);
  filter: contrast(1.05) saturate(1.1);
  position: relative;
  z-index: 1;
}

.hero__photo-glow {
  position: absolute;
  inset: -20px;
  z-index: 0;
  background: conic-gradient(from 180deg, var(--sv-red), var(--sv-purple), var(--sv-cyan), var(--sv-red));
  filter: blur(60px);
  opacity: 0.35;
}

/* ============ RESPONSIVE (mobile <= 768px) ============ */
@media (max-width: 768px) {
  .hero__inner {
    grid-template-columns: 1fr;
    text-align: center;
    gap: var(--space-md);
  }

  .hero__photo-wrap {
    order: -1;
  }

  .hero__desc {
    margin-inline: auto;
  }
}
</style>
