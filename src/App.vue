<template>
  <v-app>
    <AppHeader />
    <v-main>
      <HeroSection />
      <ServicesSection />
      <DoctorsSection />
      <StatsSection />
      <TestimonialsSection />
      <AppointmentSection />
      <ContactSection />
    </v-main>
    <AppFooter />
  </v-app>
</template>

<script setup>
import AppHeader from './components/AppHeader.vue'
import AppFooter from './components/AppFooter.vue'
import HeroSection from './components/HeroSection.vue'
import ServicesSection from './components/ServicesSection.vue'
import DoctorsSection from './components/DoctorsSection.vue'
import StatsSection from './components/StatsSection.vue'
import TestimonialsSection from './components/TestimonialsSection.vue'
import AppointmentSection from './components/AppointmentSection.vue'
import ContactSection from './components/ContactSection.vue'
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;600;700&family=DM+Sans:wght@300;400;500;600&display=swap');

:root {
  --clinic-primary: #0a6e61;
  --clinic-secondary: #12a090;
  --clinic-accent: #f4a940;
  --clinic-light: #e8f5f3;
  --clinic-dark: #062e29;
  --clinic-text: #1a2e2c;
  --clinic-muted: #6b8a87;
}

* {
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: 'DM Sans', sans-serif !important;
  color: var(--clinic-text) !important;
}

.section-title {
  font-family: 'Playfair Display', serif !important;
  font-weight: 700 !important;
  color: var(--clinic-dark) !important;
}

.section-subtitle {
  font-family: 'DM Sans', sans-serif !important;
  color: var(--clinic-muted) !important;
  font-weight: 400 !important;
}

/* Fade up animation */
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(40px); }
  to   { opacity: 1; transform: translateY(0); }
}

@keyframes fadeIn {
  from { opacity: 0; }
  to   { opacity: 1; }
}

@keyframes slideInLeft {
  from { opacity: 0; transform: translateX(-60px); }
  to   { opacity: 1; transform: translateX(0); }
}

@keyframes slideInRight {
  from { opacity: 0; transform: translateX(60px); }
  to   { opacity: 1; transform: translateX(0); }
}

@keyframes pulse-ring {
  0%   { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(18, 160, 144, 0.5); }
  70%  { transform: scale(1);    box-shadow: 0 0 0 18px rgba(18, 160, 144, 0); }
  100% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(18, 160, 144, 0); }
}

@keyframes float {
  0%, 100% { transform: translateY(0px); }
  50%       { transform: translateY(-14px); }
}

.animate-fade-up  { animation: fadeUp 0.7s ease both; }
.animate-fade-in  { animation: fadeIn 0.7s ease both; }
.animate-slide-left  { animation: slideInLeft 0.7s ease both; }
.animate-slide-right { animation: slideInRight 0.7s ease both; }
.delay-1 { animation-delay: 0.15s; }
.delay-2 { animation-delay: 0.30s; }
.delay-3 { animation-delay: 0.45s; }
.delay-4 { animation-delay: 0.60s; }
.delay-5 { animation-delay: 0.75s; }
</style>