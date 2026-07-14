# Portfolio Albany — Spider-Verse / Miles Morales Theme

SPA portfolio dibangun dengan **Vue 3 (Composition API + `<script setup>`)**,
CSS vanilla (tanpa framework eksternal), dan Vite sebagai build tool.

## Menjalankan di lokal

```bash
npm install
npm run dev
```

Buka URL yang muncul di terminal (biasanya `http://localhost:5173`).

Untuk build production:

```bash
npm run build
npm run preview   # opsional, untuk cek hasil build
```

## Struktur folder

```
src/
├── App.vue                        # shell: nav + merangkai semua section
├── style.css                      # design tokens, font, utility .sv-halftone & .sv-panel
├── main.js
└── components/
    ├── HeroSection.vue            # foto profil (mask-image) + teks glitch
    ├── AboutSection.vue           # grid deskripsi + 3 foto panel komik
    ├── ExperienceSection.vue      # sticky intro + slide foto manual + kartu
    │                               pengalaman (IntersectionObserver) + 4 tab
    │                               eksplorasi (Design/Coding/Memasak/Lainnya)
    ├── SocialSection.vue          # ikon medsos mengambang + state activeSocial
    └── ContactSection.vue         # tombol WA + form email (EmailJS)
```

## Checklist hal yang wajib kamu ganti

- [ ] **Foto profil & 3 snapshot** — di `HeroSection.vue` dan `AboutSection.vue`,
      ganti `src="https://placehold.co/..."` dengan path foto asli kamu
      (taruh filenya di folder `public/images/`, lalu referensikan sebagai
      `/images/nama-file.jpg`).
- [ ] **Nomor WhatsApp** — di `ContactSection.vue`, ganti variabel `waNumber`
      (format internasional tanpa `+`/`0` di depan, contoh: `6281234567890`).
- [ ] **Link Instagram / LinkedIn / GitHub** — di `SocialSection.vue`, array
      `socials`, ganti `USERNAME_KAMU` di tiap `href`.
- [ ] **EmailJS** — di `ContactSection.vue` fungsi `sendEmail()`, isi
      `YOUR_SERVICE_ID`, `YOUR_TEMPLATE_ID`, dan `YOUR_PUBLIC_KEY` sesuai
      dashboard [emailjs.com](https://www.emailjs.com). Template EmailJS kamu
      perlu punya variabel `user_name`, `user_email`, `message` (sudah cocok
      dengan atribut `name` di form).
  - Alternatif tanpa library JS: ada snippet Formspree yang sudah
        dikomentari langsung di dalam `ContactSection.vue`, tinggal salin-pakai.
- [ ] **Daftar pengalaman & foto slider** — di `ExperienceSection.vue`, array
      `experiences`, ganti item bertanda `[Nama Pengalaman]` beserta `photo`
      (placehold.co) dengan pengalaman & foto asli kamu. Item pertama
      ("Wakil Ketua Pelaksana — Entrepreneur Day") sudah diisi sebagai contoh.
      Slide foto di kolom kiri otomatis ikut array yang sama (navigasi manual
      lewat panah/dot, bukan auto-play), dan sinkron kalau kartu di kanan
      diklik.
- [ ] **4 menu eksplorasi (Design/Coding/Memasak/Lainnya)** — di
      `ExperienceSection.vue`, array `hobbyTabs`. Tab "Coding" sudah diisi
      dari proyek nyata; tab Design/Memasak/Lainnya masih bertanda `[...]` —
      ganti gambar & deskripsinya dengan karya/hobi asli kamu.
- [ ] **Paragraf About** — sesuaikan gaya bahasa & ceritanya biar lebih
      personal (ada penanda `TODO` di `AboutSection.vue`).

## Catatan teknis

- Halftone pattern & efek glitch/chromatic-aberration dibuat 100% CSS
  (radial-gradient + `clip-path` + `data-text`), tidak ada file gambar.
- Font display (`Bangers`) di-load dari Google Fonts via `@import` di
  `style.css`; kalau offline, otomatis fallback ke `Impact`/`Arial Black`.
- Responsif penuh mengikuti breakpoint `@media (max-width: 768px)` di
  masing-masing komponen.
- Sudah menghormati `prefers-reduced-motion` dan ada `focus-visible` untuk
  navigasi keyboard.
