<script setup>
import { ref, onMounted } from 'vue'
import emailjs from '@emailjs/browser'

// ========== KONFIGURASI EMAILJS ==========
const SERVICE_ID = 'service_upte9rc'
const TEMPLATE_ID = 'template_r22f6s9'
const PUBLIC_KEY = 'PTRymiXEmCzzB98OX'
const RECIPIENT_EMAIL = 'albanyogproperties@gmail.com'

// Ganti dengan nomor WhatsApp kamu, format internasional tanpa "+" atau "0" di depan
const waNumber = '628XXXXXXXXXX'
const waMessage = encodeURIComponent('Halo Albany, saya lihat portfolio kamu!')

const formRef = ref(null)
const status = ref('idle') // 'idle' | 'sending' | 'success' | 'error'

// Initialize EmailJS saat component mount
onMounted(() => {
  emailjs.init(PUBLIC_KEY)
})

function sendEmail() {
  status.value = 'sending'

  const templateParams = {
    from_name: formRef.value.from_name.value,
    from_email: formRef.value.from_email.value,
    message: formRef.value.message.value,
    to_email: RECIPIENT_EMAIL
  }

  emailjs
    .send(SERVICE_ID, TEMPLATE_ID, templateParams)
    .then(() => {
      status.value = 'success'
      formRef.value.reset()
      setTimeout(() => {
        status.value = 'idle'
      }, 3000)
    })
    .catch((err) => {
      console.error('EmailJS error:', err)
      status.value = 'error'
      setTimeout(() => {
        status.value = 'idle'
      }, 3000)
    })
}
</script>

<template>
  <section class="contact sv-halftone">
    <div class="contact__inner">
      <div class="contact__intro">
        <p class="sv-eyebrow">// CONTACT.SEND</p>
        <h2 class="contact__title">Mari Ngobrol</h2>
        <p class="contact__desc">
          Ada proyek, kolaborasi, atau sekadar mau say hi? Chat langsung lewat
          WhatsApp atau kirim pesan lewat form di samping.
        </p>

        <a
          class="wa-btn"
          :href="`https://wa.me/${+6285941000309}?text=${encodeURIComponent('Halo Albany, Boleh saya kenalan?')}`"
          target="_blank"
          rel="noopener noreferrer"
        >
          <svg viewBox="0 0 24 24" class="wa-btn__icon" aria-hidden="true">
            <path
              fill="currentColor"
              d="M12 2.5A9.5 9.5 0 0 0 3.6 16.9L2.5 21.5l4.7-1.2A9.5 9.5 0 1 0 12 2.5Zm0 1.7a7.8 7.8 0 0 1 6.6 12 7.8 7.8 0 0 1-11.7 2.2l-.3-.2-2.8.7.7-2.7-.2-.3A7.8 7.8 0 0 1 12 4.2Zm-2.9 4a.8.8 0 0 0-.6.3c-.2.2-.8.8-.8 1.9s.8 2.2.9 2.4c.1.1 1.6 2.5 3.9 3.5 1.9.8 2.3.7 2.7.6.4-.1 1.3-.5 1.5-1s.2-.9.1-1c-.1-.1-.2-.2-.5-.3l-1.4-.7c-.2-.1-.4-.1-.5.1l-.6.8c-.1.1-.2.2-.4.1-.2-.1-.9-.3-1.7-1-.6-.6-1-1.3-1.2-1.5-.1-.2 0-.3.1-.4l.4-.5c.1-.1.1-.3.1-.4 0-.1-.5-1.4-.7-1.9-.2-.4-.4-.4-.5-.4h-.4Z"
            />
          </svg>
          Chat via WhatsApp
        </a>
      </div>

      <!-- ============ FORM EMAIL — dikirim via EmailJS ============ -->
      <form ref="formRef" class="contact-form sv-panel">
        <div class="field">
          <label for="from_name">Nama</label>
          <input id="from_name" name="from_name" type="text" required placeholder="Nama kamu" />
        </div>

        <div class="field">
          <label for="from_email">Email</label>
          <input id="from_email" name="from_email" type="email" required placeholder="email@kamu.com" />
        </div>

        <div class="field">
          <label for="message">Pesan</label>
          <textarea id="message" name="message" rows="4" required placeholder="Tulis pesan kamu..."></textarea>
        </div>

        <button type="button" @click="sendEmail" class="submit-btn" :disabled="status === 'sending'">
          {{ status === 'sending' ? 'Mengirim...' : 'Kirim Pesan' }}
        </button>

        <p v-if="status === 'success'" class="form-note form-note--ok">Pesan terkirim, makasih! 🎉</p>
        <p v-if="status === 'error'" class="form-note form-note--err">
          Gagal terkirim — cek konsol untuk detail error (F12 → Console).
        </p>

        <!--
          ALTERNATIF TANPA JS LIBRARY (Formspree fallback):
          Kalau kamu tidak mau pakai EmailJS, ganti tag <form> di atas
          (hapus juga ref, @submit.prevent, dan hapus import emailjs
          di <script setup>) dengan versi berikut:

          <form action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
            <input type="text" name="name" placeholder="Nama" required />
            <input type="email" name="email" placeholder="Email" required />
            <textarea name="message" placeholder="Pesan" required></textarea>
            <button type="submit">Kirim Pesan</button>
          </form>

          Form ini submit biasa (reload halaman) langsung ke Formspree,
          tanpa butuh library JS apapun. Daftar & ambil YOUR_FORM_ID di
          https://formspree.io
        -->
      </form>
    </div>
  </section>
</template>

<style scoped>
.contact {
  padding: var(--space-xl) clamp(1.2rem, 4vw, 3rem) var(--space-xl);
}

.contact__inner {
  max-width: var(--section-max-width);
  margin: 0 auto;
  display: grid;
  grid-template-columns: 0.9fr 1.1fr;
  gap: var(--space-lg);
  align-items: start;
}

.contact__title {
  font-size: clamp(1.8rem, 3.5vw, 2.6rem);
  margin: 0.5rem 0 var(--space-md);
  text-shadow: 3px 0 var(--sv-red), -3px 0 var(--sv-purple);
}

.contact__desc {
  color: rgba(244, 244, 242, 0.75);
  max-width: 40ch;
  margin-bottom: var(--space-md);
}

/* ============ TOMBOL WHATSAPP ============ */
.wa-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.6rem;
  padding: 0.9rem 1.6rem;
  background: #25d366;
  color: var(--sv-ink);
  font-weight: 700;
  text-decoration: none;
  clip-path: polygon(0 0, 100% 0, 96% 100%, 4% 100%);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.wa-btn:hover {
  transform: translateY(-3px);
  box-shadow: 5px 5px 0 var(--sv-cyan);
}

.wa-btn__icon {
  width: 22px;
  height: 22px;
}

/* ============ FORM ============ */
.contact-form {
  padding: var(--space-md);
  display: flex;
  flex-direction: column;
  gap: var(--space-sm);
}

.field {
  display: flex;
  flex-direction: column;
  gap: 0.4rem;
}

.field label {
  font-family: var(--font-mono);
  font-size: 0.8rem;
  letter-spacing: 1px;
  text-transform: uppercase;
  color: var(--sv-cyan);
}

.field input,
.field textarea {
  background: var(--sv-bg);
  border: 2px solid rgba(244, 244, 242, 0.2);
  color: var(--sv-white);
  padding: 0.7rem 0.9rem;
  font-family: var(--font-body);
  font-size: 0.95rem;
  resize: vertical;
  transition: border-color 0.2s ease;
}

.field input:focus,
.field textarea:focus {
  border-color: var(--sv-red);
  outline: none;
}

.submit-btn {
  margin-top: 0.4rem;
  padding: 0.85rem 1.6rem;
  background: var(--sv-red);
  color: var(--sv-white);
  border: none;
  font-family: var(--font-mono);
  font-size: 0.9rem;
  letter-spacing: 1px;
  text-transform: uppercase;
  cursor: pointer;
  clip-path: polygon(3% 0, 100% 0, 97% 100%, 0 100%);
  transition: background 0.2s ease, transform 0.2s ease;
}

.submit-btn:hover:not(:disabled) {
  background: var(--sv-cyan);
  color: var(--sv-ink);
  transform: translateY(-2px);
}

.submit-btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.form-note {
  font-family: var(--font-mono);
  font-size: 0.85rem;
}

.form-note--ok {
  color: var(--sv-cyan);
}

.form-note--err {
  color: var(--sv-red);
}

/* ============ RESPONSIVE (mobile <= 768px) ============ */
@media (max-width: 768px) {
  .contact__inner {
    grid-template-columns: 1fr;
  }
}
</style>
