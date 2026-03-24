<template>
  <footer class="app-footer">
    <!-- Top wave -->
    <div class="footer-wave">
      <svg viewBox="0 0 1440 80" preserveAspectRatio="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M0,40 C360,100 1080,-20 1440,40 L1440,0 L0,0 Z" fill="white"/>
      </svg>
    </div>

    <v-container style="max-width:1280px">

      <!-- Main footer grid -->
      <v-row class="pt-10 pb-8">

        <!-- Brand column -->
        <v-col cols="12" md="4" class="pr-md-10">
          <div class="footer-logo d-flex align-center ga-2 mb-5">
            <div class="logo-icon">
              <v-icon icon="mdi-hospital-box" color="white" size="22" />
            </div>
            <div>
              <span class="logo-name">Vita</span><span class="logo-clinic">Clinic</span>
            </div>
          </div>
          <p class="footer-desc">
            Providing compassionate, world-class healthcare since 2008. 
            Our patients are family — your health, wellbeing, and peace of mind always come first.
          </p>
          <!-- Social icons -->
          <div class="social-row mt-6">
            <a v-for="s in socials" :key="s.icon" :href="s.href" target="_blank" class="social-link">
              <v-icon :icon="s.icon" size="20" />
            </a>
          </div>
        </v-col>

        <!-- Links columns -->
        <v-col
          v-for="col in linkCols"
          :key="col.title"
          cols="6" sm="4" md="2"
        >
          <div class="footer-col-title">{{ col.title }}</div>
          <ul class="footer-links">
            <li v-for="link in col.links" :key="link">
              <a href="#" class="footer-link">{{ link }}</a>
            </li>
          </ul>
        </v-col>

        <!-- Newsletter column -->
        <v-col cols="12" sm="12" md="4">
          <div class="footer-col-title">Health Newsletter</div>
          <p class="footer-desc mb-4">
            Get weekly health tips, clinic updates, and exclusive offers delivered to your inbox.
          </p>
          <div class="newsletter-row">
            <v-text-field
              v-model="email"
              placeholder="your@email.com"
              variant="solo"
              rounded="lg"
              hide-details
              density="comfortable"
              bg-color="rgba(255,255,255,0.1)"
              class="newsletter-input"
            />
            <v-btn
              class="subscribe-btn"
              rounded="lg"
              icon="mdi-send"
              @click="subscribe"
            />
          </div>
          <p v-if="subscribed" class="subscribed-msg mt-2">
            <v-icon icon="mdi-check-circle" size="16" /> Thanks for subscribing!
          </p>

          <!-- Certifications -->
          <div class="certs mt-6">
            <div v-for="c in certs" :key="c.label" class="cert-badge">
              <v-icon :icon="c.icon" size="16" />
              <span>{{ c.label }}</span>
            </div>
          </div>
        </v-col>

      </v-row>

      <v-divider class="footer-divider" />

      <!-- Bottom bar -->
      <div class="footer-bottom">
        <span>© {{ new Date().getFullYear() }} VitaClinic Medical Center. All rights reserved.</span>
        <div class="bottom-links">
          <a href="#" class="bottom-link">Privacy Policy</a>
          <a href="#" class="bottom-link">Terms of Use</a>
          <a href="#" class="bottom-link">Sitemap</a>
        </div>
      </div>

    </v-container>
  </footer>
</template>

<script setup>
import { ref } from 'vue'

const email = ref('')
const subscribed = ref(false)

function subscribe() {
  if (email.value) { subscribed.value = true; email.value = '' }
}

const socials = [
  { icon: 'mdi-facebook',  href: '#' },
  { icon: 'mdi-twitter',   href: '#' },
  { icon: 'mdi-instagram', href: '#' },
  { icon: 'mdi-linkedin',  href: '#' },
  { icon: 'mdi-youtube',   href: '#' },
]

const linkCols = [
  {
    title: 'Services',
    links: ['General Medicine', 'Cardiology', 'Orthopedics', 'Pediatrics', 'Neurology', 'Ophthalmology'],
  },
  {
    title: 'Clinic',
    links: ['About Us', 'Our Doctors', 'Patient Stories', 'Careers', 'News & Blog', 'Contact'],
  },
  {
    title: 'Patients',
    links: ['Book Appointment', 'Patient Portal', 'Insurance', 'FAQs', 'Emergency Care'],
  },
]

const certs = [
  { icon: 'mdi-shield-check', label: 'ISO 9001:2015' },
  { icon: 'mdi-hospital',     label: 'JCI Accredited' },
  { icon: 'mdi-lock-outline', label: 'HIPAA Compliant' },
]
</script>

<style scoped>
.app-footer {
  background: linear-gradient(160deg, var(--clinic-dark) 0%, #0d5547 100%);
  position: relative;
  overflow: hidden;
}

.footer-wave {
  line-height: 0;
  margin-bottom: -2px;
}
.footer-wave svg { width: 100%; height: 80px; }

/* Logo */
.logo-icon {
  width: 40px; height: 40px;
  background: linear-gradient(135deg, var(--clinic-secondary), #1bbfab);
  border-radius: 12px;
  display: flex; align-items: center; justify-content: center;
  box-shadow: 0 4px 14px rgba(18,160,144,0.4);
}
.logo-name  { font-family: 'Playfair Display', serif; font-size: 1.3rem; font-weight: 700; color: white; }
.logo-clinic{ font-family: 'DM Sans', sans-serif;    font-size: 1.3rem; font-weight: 300; color: rgba(255,255,255,0.6); }

.footer-desc {
  color: rgba(255,255,255,0.6);
  font-size: 0.88rem;
  line-height: 1.75;
  max-width: 300px;
}

/* Social */
.social-row { display: flex; gap: 10px; }
.social-link {
  width: 38px; height: 38px;
  border-radius: 10px;
  background: rgba(255,255,255,0.1);
  border: 1px solid rgba(255,255,255,0.15);
  display: flex; align-items: center; justify-content: center;
  color: rgba(255,255,255,0.7);
  text-decoration: none;
  transition: background 0.2s, color 0.2s, transform 0.2s;
}
.social-link:hover {
  background: var(--clinic-secondary);
  color: white;
  transform: translateY(-3px);
  border-color: var(--clinic-secondary);
}

/* Links */
.footer-col-title {
  font-family: 'DM Sans', sans-serif;
  font-weight: 700;
  font-size: 0.9rem;
  color: white;
  margin-bottom: 16px;
  letter-spacing: 0.02em;
}
.footer-links { list-style: none; padding: 0; margin: 0; display: flex; flex-direction: column; gap: 10px; }
.footer-link {
  color: rgba(255,255,255,0.58);
  font-size: 0.85rem;
  text-decoration: none;
  transition: color 0.2s, padding-left 0.2s;
}
.footer-link:hover { color: var(--clinic-secondary); padding-left: 4px; }

/* Newsletter */
.newsletter-row { display: flex; gap: 8px; }
.newsletter-input :deep(.v-field__input) { color: white !important; }
.newsletter-input :deep(.v-field__input::placeholder) { color: rgba(255,255,255,0.4) !important; }
.newsletter-input :deep(.v-field) { border: 1px solid rgba(255,255,255,0.2) !important; }

.subscribe-btn {
  background: linear-gradient(135deg, var(--clinic-secondary), #1bbfab) !important;
  color: white !important;
  min-width: 48px !important;
}
.subscribed-msg { color: #4ade80; font-size: 0.83rem; font-weight: 500; display: flex; align-items: center; gap: 6px; }

/* Certs */
.certs { display: flex; flex-wrap: wrap; gap: 8px; }
.cert-badge {
  display: flex; align-items: center; gap: 6px;
  background: rgba(255,255,255,0.08);
  border: 1px solid rgba(255,255,255,0.15);
  border-radius: 8px;
  padding: 6px 12px;
  color: rgba(255,255,255,0.65);
  font-size: 0.75rem;
  font-weight: 600;
}

/* Divider & bottom */
.footer-divider { border-color: rgba(255,255,255,0.12) !important; margin: 8px 0; }

.footer-bottom {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 12px;
  padding: 20px 0;
  color: rgba(255,255,255,0.4);
  font-size: 0.82rem;
}
.bottom-links { display: flex; gap: 20px; }
.bottom-link { color: rgba(255,255,255,0.4); text-decoration: none; transition: color 0.2s; }
.bottom-link:hover { color: var(--clinic-secondary); }
</style>