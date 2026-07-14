<script setup>
import { ref, computed } from 'vue'

/* ============================================================
   PENGALAMAN (dulu "Prestasi") — daftar diganti supaya kesannya
   berbagi wawasan/pengalaman, bukan pamer. Item pertama sudah
   diisi dengan pengalaman nyata, sisanya template — ganti
   [Nama Pengalaman] dan foto dengan milik kamu sendiri.
   ============================================================ */
const experiences = ref([
  {
    id: 1,
    title: 'Wakil Ketua Pelaksana — Entrepreneur Day',
    category: 'Kepemimpinan & Organisasi',
    desc: 'Memimpin tim pelaksana acara kewirausahaan sekolah, mulai dari penyusunan konsep, proposal sponsorship, hingga koordinasi teknis di hari-H.',
    photo: 'https://i.ibb.co.com/Df0wsSnr/Logo-EO.webp',
  },
  {
    id: 2,
    title: 'Pengurus OSIS Tahun 2024/2025/2026',
    category: 'Seksi Bidang Humas & IT (PDD)',
    desc: 'Singkat saja, #PDDSampeAjalDateng',
    photo: 'https://i.ibb.co.com/TM3xcRXf/Foto-Gw-OSISS.jpg',
  },
  {
    id: 3,
    title: 'National Forest Leadership Forum 2026',
    category: 'Delegasi Nasional',
    desc: 'Saya mengikuti forum kepemimpinan nasional yang membahas isu kehutanan dan lingkungan, mewakili sekolah saya di tingkat nasional.',
    photo: 'https://i.ibb.co.com/LXd5p7V3/Sertifikat-NFLF.jpg',
  },
  {
    id: 4,
    title: 'Joki Pembuatan Website',
    category: 'Freelance',
    desc: 'Sudah terdapat 30 projek untuk teman sekolah yaitu pembuatan website sederhana berbasis front-end dan back-end, lengkapnya di ig @albanyyog',
    photo: 'https://i.ibb.co.com/Pz4qpnpm/Joki.webp',
  },
])

/* ============================================================
   SLIDE FOTO MANUAL
   Dikontrol lewat panah/dot (tidak auto-play). Foto & judul yang
   tampil mengikuti activeIndex, dan otomatis sinkron kalau kartu
   pengalaman di kolom kanan diklik.
   ============================================================ */
const activeIndex = ref(0)
const activeExperience = computed(() => experiences.value[activeIndex.value])

function prevPhoto() {
  activeIndex.value = (activeIndex.value - 1 + experiences.value.length) % experiences.value.length
}
function nextPhoto() {
  activeIndex.value = (activeIndex.value + 1) % experiences.value.length
}

/* ============================================================
   EKSPLORASI LEBIH LANJUT — 4 menu tombol (Design/Coding/
   Memasak/Lainnya). "Coding" sudah diisi dari proyek nyata,
   3 lainnya masih template — ganti sesuai pengalaman kamu.
   ============================================================ */
const hobbyTabs = [
  {
    key: 'design',
    label: 'Design',
    accent: 'var(--sv-purple)',
    title: 'Canva Design 2025-2026',
    desc: 'Ini dia beberapa hasil design saya, selengkapnya di ig @albanyyog, thanks for help @chayamrc @maliqueh @kristohtb',
    image: '/images/Design.webp',
  },
  {
    key: 'coding',
    label: 'Coding',
    accent: 'var(--sv-cyan)',
    title: 'Dari Landing Page sampai E-Commerce',
    desc: 'Masih belajar, cukup 30 projek dulu untuk AUD tipis-tipis #AUDIZINOUT',
    image: '/images/Coding.webp',
  },
  {
    key: 'memasak',
    label: 'Memasak',
    accent: 'var(--sv-red)',
    title: 'Bisa dibilang "Noodle Specialist" hehe',
    desc: 'Suka modif atau memperbagus makanan yang biasa jadi aduhai, jujur sempet ada cita-cita jadi chef tapi terkubur, sabi kali ya sampingan chef?',
    image: '/images/Cook.webp',
  },
  {
    key: 'lainnya',
    label: 'Lainnya',
    accent: 'var(--sv-white)',
    title: 'Apa aja yang penting bukan MACEW',
    desc: '#F1Mercedez #Photographer #Videographer #Basket #Billiard #Carenthusiast #Editor #WILDEHOPPS #TouringAsik #Cedid #Novel #AI(AssettoIni)',
    image: '/images/Lainnya.webp',
  },
]

const activeHobbyKey = ref('design')
const activeHobby = computed(() => hobbyTabs.find((tab) => tab.key === activeHobbyKey.value))
</script>

<template>
  <section class="experience sv-halftone">
    <div class="experience__inner">
      <!-- ============ KOLOM KIRI — sticky, deskripsi + slide foto manual ============ -->
      <div class="experience__intro">
        <p class="sv-eyebrow">// AkuBukan.pdf</p>
        <h2 class="experience__title">Jejak Pengalaman</h2>
        <p class="experience__desc">
          Kumpulan pengalaman, tanggung jawab, dan wawasan yang sudah saya
          jalani dari organisasi hingga pencapaian berupa sertifikat. Scroll ke
          kanan atau klik kartunya untuk lihat satu per satu. Masih dikit nyak hehe semoga
          tahun ini nambah lagi Aamiin.
        </p>

        <!-- ==================== SLIDE FOTO MANUAL ====================
             Navigasi lewat panah/dot saja (tidak auto-play). Foto & judul
             ikut activeIndex, dan klik kartu di kolom kanan akan
             menyinkronkan slide ini ke pengalaman yang sesuai.
        =================================================================== -->
        <div class="photo-slider">
          <div class="photo-slider__stage">
            <div class="photo-slider__frame sv-panel">
              <img :src="activeExperience.photo" :alt="activeExperience.title" />
            </div>
            <p class="photo-slider__caption">{{ activeExperience.title }}</p>
          </div>

          <div class="photo-slider__controls">
            <button class="photo-slider__arrow" aria-label="Foto sebelumnya" @click="prevPhoto">‹</button>

            <div class="photo-slider__dots">
              <button
                v-for="(exp, i) in experiences"
                :key="exp.id"
                class="photo-slider__dot"
                :class="{ 'is-active': i === activeIndex }"
                :aria-label="`Lihat foto: ${exp.title}`"
                @click="activeIndex = i"
              ></button>
            </div>

            <button class="photo-slider__arrow" aria-label="Foto berikutnya" @click="nextPhoto">›</button>
          </div>
        </div>
      </div>

      <!-- ============ KOLOM KANAN — list kartu pengalaman ============ -->
      <div class="experience__list">
        <article
          v-for="(item, index) in experiences"
          :key="item.id"
          class="experience-card"
          @click="activeIndex = index"
        >
          <span class="experience-card__category">{{ item.category }}</span>
          <h3 class="experience-card__title">{{ item.title }}</h3>
          <p class="experience-card__desc">{{ item.desc }}</p>
        </article>
      </div>
    </div>

    <!-- ==================== EKSPLORASI LEBIH LANJUT ====================
         Prompt + 4 tombol menu (Design/Coding/Memasak/Lainnya), isinya
         berupa gambar + deskripsi kegiatan sesuai tab yang dipilih.
    =================================================================== -->
    <div class="explore">
      <div class="explore__prompt">
        <p class="explore__text">Mau tahu lebih banyak? Klik menu di samping:</p>

        <div class="explore__tabs" role="tablist" aria-label="Pilih kategori eksplorasi">
          <button
            v-for="tab in hobbyTabs"
            :key="tab.key"
            class="explore-tab"
            :class="{ 'is-active': activeHobbyKey === tab.key }"
            :style="{ '--tab-accent': tab.accent }"
            role="tab"
            :aria-selected="activeHobbyKey === tab.key"
            @click="activeHobbyKey = tab.key"
          >
            {{ tab.label }}
          </button>
        </div>
      </div>

      <Transition name="fade" mode="out-in">
        <div
          :key="activeHobby.key"
          class="explore-panel sv-panel"
          :style="{ '--tab-accent': activeHobby.accent }"
          role="tabpanel"
        >
          <div class="explore-panel__media">
            <img :src="activeHobby.image" :alt="activeHobby.title" />
          </div>
          <div class="explore-panel__text">
            <span class="sv-eyebrow">{{ activeHobby.label }}</span>
            <h3>{{ activeHobby.title }}</h3>
            <p>{{ activeHobby.desc }}</p>
          </div>
        </div>
      </Transition>
    </div>
  </section>
</template>

<style scoped>
.experience {
  padding: var(--space-xl) clamp(1.2rem, 4vw, 3rem);
}

.experience__inner {
  max-width: var(--section-max-width);
  margin: 0 auto;
  display: grid;
  grid-template-columns: 0.8fr 1.2fr;
  gap: var(--space-lg);
  align-items: start;
}

/* ============ KOLOM KIRI — STICKY ============ */
.experience__intro {
  position: sticky;
  top: 20px;
}

.experience__title {
  font-size: clamp(1.8rem, 3.5vw, 2.6rem);
  margin: 0.5rem 0 var(--space-md);
  text-shadow: 3px 0 var(--sv-purple), -3px 0 var(--sv-cyan);
}

.experience__desc {
  color: rgba(244, 244, 242, 0.75);
  max-width: 36ch;
}

/* ============ SLIDE FOTO MANUAL ============ */
.photo-slider {
  margin-top: var(--space-md);
  max-width: 320px;
}

.photo-slider__stage {
  display: block;
}

.photo-slider__frame {
  padding: 6px;
}

.photo-slider__frame img {
  width: 100%;
  aspect-ratio: 4 / 3;
  object-fit: cover;
}

.photo-slider__caption {
  margin-top: 0.7rem;
  font-family: var(--font-mono);
  font-size: 0.85rem;
  color: var(--sv-cyan);
  min-height: 2.4em;
}

.photo-slider__controls {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 0.6rem;
  margin-top: 0.5rem;
}

.photo-slider__arrow {
  width: 32px;
  height: 32px;
  flex-shrink: 0;
  border: 2px solid rgba(244, 244, 242, 0.3);
  background: transparent;
  color: var(--sv-white);
  font-size: 1.1rem;
  line-height: 1;
  cursor: pointer;
  transition: border-color 0.2s ease, color 0.2s ease, transform 0.2s ease;
}

.photo-slider__arrow:hover {
  border-color: var(--sv-red);
  color: var(--sv-red);
  transform: scale(1.08);
}

.photo-slider__dots {
  display: flex;
  gap: 0.4rem;
}

.photo-slider__dot {
  width: 9px;
  height: 9px;
  border-radius: 50%;
  border: none;
  background: rgba(244, 244, 242, 0.25);
  cursor: pointer;
  padding: 0;
  transition: background 0.2s ease, transform 0.2s ease;
}

.photo-slider__dot.is-active {
  background: var(--sv-red);
  transform: scale(1.3);
}

/* ============ KOLOM KANAN — LIST KARTU ============ */
.experience__list {
  display: flex;
  flex-direction: column;
  gap: var(--space-md);
}

.experience-card {
  padding: var(--space-md);
  border-left: 4px solid var(--sv-red);
  background: var(--sv-bg-panel);
  clip-path: polygon(0 0, 100% 0, 100% 92%, 97% 100%, 0 100%);
  cursor: pointer;
  transition: border-color 0.25s ease, background 0.25s ease;
}

.experience-card:hover {
  background: #1d1d22;
}

.experience-card__category {
  display: inline-block;
  font-family: var(--font-mono);
  font-size: 0.75rem;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--sv-cyan);
  margin-bottom: 0.5rem;
}

.experience-card__title {
  font-family: var(--font-body);
  font-weight: 700;
  font-size: 1.2rem;
  margin-bottom: 0.4rem;
}

.experience-card__desc {
  color: rgba(244, 244, 242, 0.7);
  font-size: 0.95rem;
}

/* ============ EKSPLORASI LEBIH LANJUT ============ */
.explore {
  max-width: var(--section-max-width);
  margin: var(--space-xl) auto 0;
  padding-top: var(--space-lg);
  border-top: 1px solid rgba(244, 244, 242, 0.08);
}

.explore__prompt {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: var(--space-sm);
  margin-bottom: var(--space-md);
}

.explore__text {
  font-family: var(--font-display);
  font-size: clamp(1.2rem, 2.5vw, 1.6rem);
  letter-spacing: 0.5px;
}

.explore__tabs {
  display: flex;
  flex-wrap: wrap;
  gap: 0.7rem;
}

.explore-tab {
  --tab-accent: var(--sv-cyan);
  padding: 0.65rem 1.3rem;
  background: transparent;
  border: 2px solid var(--tab-accent);
  color: var(--tab-accent);
  font-family: var(--font-mono);
  font-size: 0.85rem;
  letter-spacing: 1px;
  text-transform: uppercase;
  cursor: pointer;
  clip-path: polygon(0 0, 100% 0, 94% 100%, 6% 100%);
  transition: background 0.2s ease, color 0.2s ease, transform 0.2s ease;
}

.explore-tab:hover {
  transform: translateY(-2px);
}

.explore-tab.is-active {
  background: var(--tab-accent);
  color: var(--sv-ink);
}

.explore-panel {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 0;
  overflow: hidden;
  box-shadow: 6px 6px 0 var(--tab-accent, var(--sv-red));
}

.explore-panel__media img {
  width: 100%;
  height: 100%;
  aspect-ratio: 4 / 3;
  object-fit: contain;
  object-position: center;
  background: var(--sv-bg);
}

.explore-panel__text {
  padding: var(--space-md);
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 0.6rem;
}

.explore-panel__text h3 {
  font-family: var(--font-body);
  font-weight: 700;
  font-size: 1.3rem;
}

.explore-panel__text p {
  color: rgba(244, 244, 242, 0.75);
  font-size: 0.95rem;
}

/* Transisi fade saat ganti tab */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.25s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

/* ============ RESPONSIVE (mobile <= 768px) ============ */
@media (max-width: 768px) {
  .experience__inner {
    grid-template-columns: 1fr;
  }

  .experience__intro {
    position: static;
  }

  .photo-slider {
    max-width: 100%;
  }

  .explore__prompt {
    flex-direction: column;
    align-items: flex-start;
  }

  .explore-panel {
    grid-template-columns: 1fr;
  }
}
</style>
