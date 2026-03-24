<template>
  <v-app-bar
    :elevation="scrolled ? 4 : 0"
    :color="scrolled ? 'white' : 'transparent'"
    class="app-header"
    height="72"
    fixed
  >
    <v-container class="d-flex align-center py-0" style="max-width: 1280px">
      <!-- Logo -->
      <div
        class="logo d-flex align-center ga-2"
        @click="scrollTo('hero')"
        style="cursor: pointer"
      >
        <div class="logo-icon">
          <v-icon icon="mdi-hospital-box" color="white" size="22" />
        </div>
        <div class="logo-text">
          <span class="logo-name">SR</span>
          <span class="logo-clinic">Clinic</span>
        </div>
      </div>

      <v-spacer />

      <!-- Desktop Nav -->
      <nav class="d-none d-md-flex align-center ga-1">
        <v-btn
          v-for="link in navLinks"
          :key="link.id"
          variant="text"
          class="nav-btn"
          :color="getNavColor(link.id)"
          @click="scrollTo(link.id)"
        >
          {{ link.label }}
        </v-btn>
      </nav>

      <v-spacer class="d-none d-md-flex" />

      <!-- CTA -->
      <v-btn
        class="d-none d-md-flex cta-btn ml-4"
        rounded="lg"
        prepend-icon="mdi-calendar-check"
        @click="scrollTo('appointment')"
      >
        Book Appointment
      </v-btn>

      <!-- Mobile menu -->
      <v-app-bar-nav-icon
        class="d-flex d-md-none"
        @click="mobileMenu = !mobileMenu"
        :color="scrolled ? 'primary' : 'white'"
      />
    </v-container>
  </v-app-bar>

  <!-- Mobile Drawer -->
  <v-navigation-drawer
    v-model="mobileMenu"
    temporary
    location="right"
    width="280"
  >
    <div class="pa-6">
      <div class="logo d-flex align-center ga-2 mb-8">
        <div class="logo-icon">
          <v-icon icon="mdi-hospital-box" color="white" size="20" />
        </div>
        <div class="logo-text">
          <span class="logo-name">SR</span>
          <span class="logo-clinic">Clinic</span>
        </div>
      </div>

      <v-list nav density="compact">
        <v-list-item
          v-for="link in navLinks"
          :key="link.id"
          :prepend-icon="link.icon"
          :title="link.label"
          @click="handleMobileClick(link.id)"
          rounded="lg"
          class="mb-1 mobile-nav-item"
        />
      </v-list>

      <v-btn
        class="cta-btn mt-6 w-100"
        rounded="lg"
        prepend-icon="mdi-calendar-check"
        @click="handleMobileClick('appointment')"
      >
        Book Appointment
      </v-btn>
    </div>
  </v-navigation-drawer>
</template>
<script setup>
  import { ref, onMounted, onUnmounted } from 'vue'

  const scrolled = ref(false)
  const mobileMenu = ref(false)
  const activeSection = ref('hero')

  const navLinks = [
    { id: 'services', label: 'Services', icon: 'mdi-medical-bag' },
    { id: 'doctors', label: 'Doctors', icon: 'mdi-doctor' },
    { id: 'stats', label: 'About', icon: 'mdi-information-outline' },
    { id: 'testimonials', label: 'Reviews', icon: 'mdi-star-outline' },
    { id: 'contact', label: 'Contact', icon: 'mdi-phone-outline' }
  ]

  // Scroll function
  function scrollTo(id) {
    const el = document.getElementById(id)
    if (el) {
      el.scrollIntoView({ behavior: 'smooth' })
    }
  }

  // Mobile click helper
  function handleMobileClick(id) {
    scrollTo(id)
    mobileMenu.value = false
  }

  // 🎯 Dynamic color (FIXED)
  function getNavColor(id) {
    if (activeSection.value === id) return 'secondary'
    return scrolled.value ? 'default' : 'white'
  }

  // Scroll listener (IMPROVED)
  function onScroll() {
    scrolled.value = window.scrollY > 50

    for (const link of [...navLinks].reverse()) {
      const el = document.getElementById(link.id)
      if (el && window.scrollY + 150 >= el.offsetTop) {
        activeSection.value = link.id
        break
      }
    }
  }

  onMounted(() => window.addEventListener('scroll', onScroll))
  onUnmounted(() => window.removeEventListener('scroll', onScroll))
</script>
<style scoped>
  .app-header {
    transition: all 0.35s ease;
  }

  /* Logo */
  .logo-icon {
    width: 38px;
    height: 38px;
    background: linear-gradient(
      135deg,
      var(--clinic-primary),
      var(--clinic-secondary)
    );
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: 0 4px 14px rgba(10, 110, 97, 0.4);
  }

  .logo-name {
    font-family: 'Playfair Display', serif;
    font-weight: 700;
    font-size: 1.3rem;
    color: var(--clinic-primary);
  }

  .logo-clinic {
    font-family: 'DM Sans', sans-serif;
    font-weight: 300;
    font-size: 1.3rem;
    color: var(--clinic-muted);
  }

  /* Nav */
  .nav-btn {
    font-family: 'DM Sans', sans-serif !important;
    font-weight: 500 !important;
    font-size: 0.9rem !important;
    text-transform: none !important;
  }

  /* CTA */
  .cta-btn {
    background: linear-gradient(
      135deg,
      var(--clinic-primary),
      var(--clinic-secondary)
    ) !important;
    color: white !important;
    font-weight: 600 !important;
    text-transform: none !important;
    box-shadow: 0 4px 16px rgba(10, 110, 97, 0.35) !important;
  }

  .cta-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 24px rgba(10, 110, 97, 0.45) !important;
  }

  .mobile-nav-item {
    font-family: 'DM Sans', sans-serif !important;
  }
</style>
