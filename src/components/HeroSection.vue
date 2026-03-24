<template>
  <section id="hero" class="hero-section">
    <!-- Background blobs -->
    <div class="blob blob-1" />
    <div class="blob blob-2" />
    <div class="blob blob-3" />

    <v-container style="max-width:1280px; position:relative; z-index:2;">
      <v-row align="center" justify="center" class="min-h-hero">

        <!-- Left content -->
        <v-col cols="12" md="6" class="hero-content">
          <div class="badge-pill animate-fade-up">
            <v-icon icon="mdi-check-decagram" size="14" color="var(--clinic-secondary)" class="mr-1" />
            Trusted Healthcare Since 2008
          </div>

          <h1 class="hero-title animate-fade-up delay-1">
            Your Health,<br>
            <span class="hero-title-accent">Our Priority</span>
          </h1>

          <p class="hero-desc animate-fade-up delay-2">
            VitaClinic provides world-class medical care with compassionate doctors, 
            advanced technology, and a patient-first approach — all under one roof.
          </p>

          <div class="d-flex flex-wrap ga-3 animate-fade-up delay-3">
            <v-btn
              class="hero-btn-primary"
              size="large"
              rounded="xl"
              prepend-icon="mdi-calendar-check-outline"
              @click="scrollTo('appointment')"
            >
              Book Appointment
            </v-btn>
            <v-btn
              class="hero-btn-secondary"
              size="large"
              rounded="xl"
              prepend-icon="mdi-play-circle-outline"
            >
              Watch Our Story
            </v-btn>
          </div>

          <!-- Trust badges -->
          <div class="trust-row animate-fade-up delay-4">
            <div v-for="t in trust" :key="t.label" class="trust-item">
              <v-icon :icon="t.icon" color="var(--clinic-secondary)" size="20" />
              <span>{{ t.label }}</span>
            </div>
          </div>
        </v-col>

        <!-- Right image card -->
        <v-col cols="12" md="6" class="d-flex justify-center position-relative animate-slide-right delay-2">
          <div class="hero-image-wrap">
            <!-- Main image -->
            <div class="hero-img-card">
              <img
                src="https://images.unsplash.com/photo-1576091160550-2173dba999ef?w=600&q=80"
                alt="Doctor"
                class="hero-img"
              />
              <div class="img-overlay" />
            </div>

            <!-- Floating cards -->
            <div class="float-card card-patients animate-float">
              <div class="float-icon bg-green">
                <v-icon icon="mdi-account-group" color="white" size="20" />
              </div>
              <div>
                <div class="float-value">12K+</div>
                <div class="float-label">Happy Patients</div>
              </div>
            </div>

            <div class="float-card card-rating animate-float delay-2">
              <div class="float-icon bg-amber">
                <v-icon icon="mdi-star" color="white" size="20" />
              </div>
              <div>
                <div class="float-value">4.9★</div>
                <div class="float-label">Patient Rating</div>
              </div>
            </div>

            <div class="float-card card-experience animate-float delay-4">
              <div class="float-icon bg-teal">
                <v-icon icon="mdi-medal-outline" color="white" size="20" />
              </div>
              <div>
                <div class="float-value">15+ Yrs</div>
                <div class="float-label">Experience</div>
              </div>
            </div>

            <!-- Pulse dot -->
            <div class="live-dot">
              <span class="pulse-ring" />
              <span class="dot-inner" />
              <span class="live-label">Live Support</span>
            </div>
          </div>
        </v-col>

      </v-row>
    </v-container>

    <!-- Wave divider -->
    <div class="hero-wave">
      <svg viewBox="0 0 1440 90" preserveAspectRatio="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M0,60 C360,120 1080,0 1440,60 L1440,90 L0,90 Z" fill="white"/>
      </svg>
    </div>
  </section>
</template>

<script setup>
const trust = [
  { icon: 'mdi-shield-check-outline', label: 'ISO Certified' },
  { icon: 'mdi-clock-fast',           label: '24/7 Emergency' },
  { icon: 'mdi-stethoscope',          label: '50+ Specialists' },
]

function scrollTo(id) {
  const el = document.getElementById(id)
  if (el) el.scrollIntoView({ behavior: 'smooth' })
}
</script>

<style scoped>
.hero-section {
  min-height: 100vh;
  background: linear-gradient(135deg, var(--clinic-dark) 0%, var(--clinic-primary) 55%, #1bbfab 100%);
  position: relative;
  overflow: hidden;
  display: flex;
  align-items: center;
  padding-top: 72px;
}

.min-h-hero { min-height: calc(100vh - 72px); padding: 80px 0 100px; }

/* Blobs */
.blob {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  opacity: 0.18;
  animation: float 8s ease-in-out infinite;
}
.blob-1 { width:500px; height:500px; background:#34d9c3; top:-120px; right:-100px; animation-delay:0s; }
.blob-2 { width:360px; height:360px; background:#f4a940; bottom:80px; left:-80px; animation-delay:3s; }
.blob-3 { width:260px; height:260px; background:#ffffff; top:40%; left:35%; animation-delay:5s; }

/* Badge */
.badge-pill {
  display: inline-flex;
  align-items: center;
  background: rgba(255,255,255,0.15);
  backdrop-filter: blur(12px);
  border: 1px solid rgba(255,255,255,0.25);
  color: white;
  border-radius: 50px;
  padding: 6px 16px;
  font-size: 0.8rem;
  font-weight: 500;
  margin-bottom: 24px;
  letter-spacing: 0.02em;
}

/* Title */
.hero-title {
  font-family: 'Playfair Display', serif !important;
  font-size: clamp(2.6rem, 5vw, 4.2rem);
  font-weight: 700;
  color: white;
  line-height: 1.15;
  margin-bottom: 20px;
}
.hero-title-accent {
  background: linear-gradient(90deg, #f4a940, #ffd37a);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero-desc {
  color: rgba(255,255,255,0.8);
  font-size: 1.05rem;
  line-height: 1.75;
  max-width: 480px;
  margin-bottom: 36px;
}

/* Buttons */
.hero-btn-primary {
  background: white !important;
  color: var(--clinic-primary) !important;
  font-weight: 600 !important;
  text-transform: none !important;
  letter-spacing: 0 !important;
  box-shadow: 0 8px 28px rgba(0,0,0,0.2) !important;
  transition: transform 0.2s, box-shadow 0.2s !important;
}
.hero-btn-primary:hover { transform: translateY(-3px); box-shadow: 0 14px 36px rgba(0,0,0,0.28) !important; }

.hero-btn-secondary {
  background: rgba(255,255,255,0.12) !important;
  color: white !important;
  font-weight: 500 !important;
  text-transform: none !important;
  letter-spacing: 0 !important;
  border: 1px solid rgba(255,255,255,0.3) !important;
  backdrop-filter: blur(8px);
  transition: background 0.2s !important;
}
.hero-btn-secondary:hover { background: rgba(255,255,255,0.22) !important; }

/* Trust badges */
.trust-row {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  margin-top: 40px;
}
.trust-item {
  display: flex;
  align-items: center;
  gap: 8px;
  color: rgba(255,255,255,0.85);
  font-size: 0.88rem;
  font-weight: 500;
}

/* Image card */
.hero-image-wrap { position: relative; width: 420px; max-width: 100%; }
.hero-img-card {
  border-radius: 28px;
  overflow: hidden;
  box-shadow: 0 30px 80px rgba(0,0,0,0.35);
  position: relative;
}
.hero-img { width: 100%; height: 500px; object-fit: cover; display: block; }
.img-overlay {
  position: absolute; inset: 0;
  background: linear-gradient(to bottom, transparent 50%, rgba(6,46,41,0.55) 100%);
}

/* Float cards */
.float-card {
  position: absolute;
  background: white;
  border-radius: 16px;
  padding: 14px 18px;
  display: flex;
  align-items: center;
  gap: 12px;
  box-shadow: 0 16px 40px rgba(0,0,0,0.18);
}
.float-card.card-patients { bottom: 60px; left: -40px; }
.float-card.card-rating   { top: 50px; right: -30px; }
.float-card.card-experience { bottom: 180px; right: -40px; }

.float-icon {
  width: 42px; height: 42px;
  border-radius: 12px;
  display: flex; align-items: center; justify-content: center;
  flex-shrink: 0;
}
.bg-green { background: linear-gradient(135deg, var(--clinic-primary), var(--clinic-secondary)); }
.bg-amber { background: linear-gradient(135deg, #f4a940, #e07b10); }
.bg-teal  { background: linear-gradient(135deg, #12a090, #0e7a6e); }

.float-value { font-size: 1rem; font-weight: 700; color: var(--clinic-dark); line-height: 1.2; }
.float-label { font-size: 0.72rem; color: var(--clinic-muted); font-weight: 400; }

/* Pulse / Live dot */
.live-dot {
  position: absolute;
  top: 22px;
  left: -20px;
  display: flex;
  align-items: center;
  gap: 8px;
  background: white;
  border-radius: 50px;
  padding: 8px 14px 8px 8px;
  box-shadow: 0 8px 24px rgba(0,0,0,0.15);
}
.pulse-ring {
  display: block;
  width: 12px; height: 12px;
  border-radius: 50%;
  background: #22c55e;
  position: relative;
  animation: pulse-ring 2s ease-out infinite;
}
.dot-inner { display: none; }
.live-label { font-size: 0.78rem; font-weight: 600; color: var(--clinic-dark); }

/* Float animation */
.animate-float { animation: float 5s ease-in-out infinite; }

/* Wave divider */
.hero-wave {
  position: absolute;
  bottom: -2px; left: 0; right: 0;
  line-height: 0;
}
.hero-wave svg { width: 100%; height: 90px; }

@media (max-width: 960px) {
  .hero-image-wrap { width: 300px; margin-top: 40px; }
  .hero-img { height: 360px; }
  .float-card.card-patients { left: -10px; }
  .float-card.card-rating   { right: -10px; }
  .float-card.card-experience { right: -10px; }
}
</style>