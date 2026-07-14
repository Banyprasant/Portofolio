<script setup>
const snapshots = [
  { id: 1, src: 'public/images/FotoSnap3.webp', alt: 'Cuplikan momen Albany 1' },
  { id: 2, src: 'public/images/FotoSnap2.webp', alt: 'Cuplikan momen Albany 2' },
  { id: 3, src: 'public/images/FotoSnap1.webp', alt: 'Cuplikan momen Albany 3' },
]
</script>

<template>
  <section class="about">
    <div class="about__inner">
      <div class="about__text">
        <p class="sv-eyebrow">// ABOUTYOU.EA</p>
        <h2 class="about__title">Sekilas Tentang Saya</h2>

        <!-- TODO: sesuaikan paragraf ini dengan cerita & gaya bahasa kamu sendiri -->
        <p class="about__desc">
          Hola, Yo Soy Albany! Siswa aktif kelas 12 di SMA Negeri 10 Tangerang Selatan. Saya suka dalam mengubah keadaan
          seperti mencairkan suasana, mengubah ide menjadi karya, dan memiliki rasa ingin tahu. Saya dominan lebih suka mendengar daripada
          berbicara karena saya suka dengan teknik DENGAR lalu PILAH. Yang dimaksud adalah kita menampung semua pendapat lalu kita ambil
          kata kunci yang krusial, lalu jadikan sebagai pelajaran. I also still learning 3 language which is english, hablas espanol y boso jowo sisan.
        </p>
        <p class="about__desc">
         Dibalik itu saya tidak suka marah-marah karena ya ngapain gitu menghabiskan energi untuk hal yang belum tentu terselesaikan
         dengan jelas, intinya gunakan iq+ketenangan jika tidak mau panic attack (Guwah Ekstrovert kondisional)
        </p>
      </div>

      <div class="about__gallery">
        <div
          v-for="(photo, index) in snapshots"
          :key="photo.id"
          class="comic-frame"
          :class="`comic-frame--${index + 1}`"
        >
          <img :src="photo.src" :alt="photo.alt" />
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.about {
  padding: var(--space-xl) clamp(1.2rem, 4vw, 3rem);
  background: var(--sv-bg);
}

.about__inner {
  max-width: var(--section-max-width);
  margin: 0 auto;
  display: grid;
  grid-template-columns: 0.95fr 1.05fr;
  gap: var(--space-lg);
  align-items: center;
}

.about__title {
  font-size: clamp(1.8rem, 3.5vw, 2.6rem);
  margin: 0.5rem 0 var(--space-md);
  text-shadow: 3px 0 var(--sv-red), -3px 0 var(--sv-cyan);
}

.about__desc {
  color: rgba(244, 244, 242, 0.78);
  margin-bottom: var(--space-sm);
}

/* ============ GALERI FOTO — PANEL KOMIK ============ */
.about__gallery {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: var(--space-md) var(--space-sm);
  padding: var(--space-sm);
}

.comic-frame {
  border: 4px solid var(--sv-white);
  box-shadow: 8px 8px 0 var(--sv-red);
  overflow: hidden;
  transform: skew(-3deg) rotate(-2deg);
  transition: transform 0.25s ease, box-shadow 0.25s ease;
}

.comic-frame img {
  width: 100%;
  height: 100%;
  aspect-ratio: 4 / 5;
  object-fit: cover;
  transform: skew(3deg) rotate(2deg) scale(1.15);
}

.comic-frame:hover {
  transform: skew(0deg) rotate(0deg) translateY(-6px);
  box-shadow: 10px 10px 0 var(--sv-cyan);
}

/* Variasi kecil supaya tidak terlalu simetris — ala tempelan panel komik */
.comic-frame--1 {
  grid-column: 1 / 2;
  grid-row: 1 / 3;
}

.comic-frame--2 {
  grid-column: 2 / 3;
  grid-row: 1 / 2;
  transform: skew(3deg) rotate(2deg);
  box-shadow: -8px 8px 0 var(--sv-cyan);
}

.comic-frame--2 img {
  transform: skew(-3deg) rotate(-2deg) scale(1.15);
}

.comic-frame--3 {
  grid-column: 2 / 3;
  grid-row: 2 / 3;
  transform: skew(-2deg) rotate(3deg);
  box-shadow: 8px -8px 0 var(--sv-purple);
}

/* ============ RESPONSIVE (mobile <= 768px) ============ */
@media (max-width: 768px) {
  .about__inner {
    grid-template-columns: 1fr;
    display: flex;
    flex-direction: column;
    gap: var(--space-lg);
  }

  .about__gallery {
    grid-template-columns: repeat(2, 1fr);
  }

  .comic-frame,
  .comic-frame--1,
  .comic-frame--2,
  .comic-frame--3 {
    transform: skew(-2deg) rotate(-1deg);
  }

  .comic-frame--1 {
    grid-column: 1 / 3;
    grid-row: auto;
  }

  .comic-frame--2,
  .comic-frame--3 {
    grid-column: span 1;
    grid-row: auto;
  }
}
</style>
