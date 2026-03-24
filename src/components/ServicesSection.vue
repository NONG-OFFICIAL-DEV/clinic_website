<template>
  <section id="services" class="services-section py-20" ref="sectionRef">
    <v-container style="max-width:1280px">

      <!-- Header -->
      <div class="text-center mb-14">
        <div class="section-badge animate-fade-up" :class="{ visible: inView }">Our Specialties</div>
        <h2 class="section-title text-h3 mt-3 animate-fade-up delay-1" :class="{ visible: inView }">
          Comprehensive Care, <br class="d-none d-sm-block">Every Step of the Way
        </h2>
        <p class="section-subtitle mt-4 mx-auto animate-fade-up delay-2" :class="{ visible: inView }" style="max-width:540px">
          From preventive check-ups to complex surgeries, our specialist teams 
          deliver evidence-based treatment tailored to you.
        </p>
      </div>

      <!-- Service cards -->
      <v-row>
        <v-col
          v-for="(s, i) in services"
          :key="s.title"
          cols="12" sm="6" lg="4"
        >
          <v-card
            :class="['service-card', `delay-${i % 3 + 1}`, { visible: inView }]"
            rounded="xl"
            flat
            @mouseenter="s.hovered = true"
            @mouseleave="s.hovered = false"
          >
            <div class="card-icon-wrap" :style="{ background: s.bg }">
              <v-icon :icon="s.icon" color="white" size="32" />
            </div>
            <div class="pa-6 pt-4">
              <div class="card-title">{{ s.title }}</div>
              <div class="card-desc">{{ s.desc }}</div>
              <ul class="card-features">
                <li v-for="f in s.features" :key="f">
                  <v-icon icon="mdi-check-circle" size="14" color="var(--clinic-secondary)" />
                  {{ f }}
                </li>
              </ul>
              <v-btn
                variant="text"
                class="learn-more-btn mt-2 pa-0"
                append-icon="mdi-arrow-right"
              >
                Learn More
              </v-btn>
            </div>
          </v-card>
        </v-col>
      </v-row>

    </v-container>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const sectionRef = ref(null)
const inView = ref(false)

const services = ref([
  {
    title: 'General Medicine',
    desc: 'Comprehensive primary care for all ages, from routine check-ups to managing chronic conditions.',
    icon: 'mdi-stethoscope',
    bg: 'linear-gradient(135deg,#0a6e61,#12a090)',
    features: ['Annual wellness exams', 'Chronic disease management', 'Preventive screenings'],
    hovered: false,
  },
  {
    title: 'Cardiology',
    desc: 'Advanced heart care using cutting-edge diagnostics and minimally invasive procedures.',
    icon: 'mdi-heart-pulse',
    bg: 'linear-gradient(135deg,#d72660,#f45d96)',
    features: ['ECG & Echo', 'Stress testing', 'Cardiac rehab'],
    hovered: false,
  },
  {
    title: 'Orthopedics',
    desc: 'Expert care for bones, joints, and muscles with both surgical and non-surgical options.',
    icon: 'mdi-bone',
    bg: 'linear-gradient(135deg,#5b2fc9,#8a63d2)',
    features: ['Joint replacement', 'Sports injuries', 'Spine surgery'],
    hovered: false,
  },
  {
    title: 'Pediatrics',
    desc: 'Dedicated care for children from newborns to teenagers in a fun, child-friendly environment.',
    icon: 'mdi-baby-face-outline',
    bg: 'linear-gradient(135deg,#e07b10,#f4a940)',
    features: ['Vaccination programs', 'Growth monitoring', 'Child nutrition'],
    hovered: false,
  },
  {
    title: 'Neurology',
    desc: 'Diagnosis and treatment of brain, spinal cord, and nervous system disorders by top specialists.',
    icon: 'mdi-brain',
    bg: 'linear-gradient(135deg,#047857,#059669)',
    features: ['MRI & CT scan', 'Epilepsy care', 'Stroke treatment'],
    hovered: false,
  },
  {
    title: 'Ophthalmology',
    desc: 'Complete eye care from prescriptions to laser surgery and treatment of eye diseases.',
    icon: 'mdi-eye-outline',
    bg: 'linear-gradient(135deg,#0369a1,#0ea5e9)',
    features: ['LASIK surgery', 'Retinal care', 'Glaucoma treatment'],
    hovered: false,
  },
])

onMounted(() => {
  const obs = new IntersectionObserver(
    ([entry]) => { if (entry.isIntersecting) inView.value = true },
    { threshold: 0.1 }
  )
  if (sectionRef.value) obs.observe(sectionRef.value)
})
</script>

<style scoped>
.services-section { background: #fff; }

.section-badge {
  display: inline-block;
  background: var(--clinic-light);
  color: var(--clinic-primary);
  font-weight: 600;
  font-size: 0.82rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  border-radius: 50px;
  padding: 6px 18px;
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.6s ease, transform 0.6s ease;
}
.section-badge.visible { opacity: 1; transform: translateY(0); }

.animate-fade-up { opacity: 0; transform: translateY(30px); transition: opacity 0.7s ease, transform 0.7s ease; }
.animate-fade-up.visible { opacity: 1; transform: translateY(0); }
.delay-1 { transition-delay: 0.15s; }
.delay-2 { transition-delay: 0.30s; }
.delay-3 { transition-delay: 0.45s; }

/* Service card */
.service-card {
  background: #fff;
  border: 1px solid #e8f5f3;
  box-shadow: 0 4px 24px rgba(10,110,97,0.07);
  transition: transform 0.35s ease, box-shadow 0.35s ease, opacity 0.7s ease;
  opacity: 0;
  transform: translateY(40px);
  overflow: visible;
  height: 100%;
}
.service-card.visible { opacity: 1; transform: translateY(0); }
.service-card:hover {
  transform: translateY(-8px) !important;
  box-shadow: 0 20px 50px rgba(10,110,97,0.15) !important;
}

.card-icon-wrap {
  width: 64px; height: 64px;
  border-radius: 18px;
  display: flex; align-items: center; justify-content: center;
  margin: 24px 24px 0;
  box-shadow: 0 8px 20px rgba(0,0,0,0.15);
  transition: transform 0.3s;
}
.service-card:hover .card-icon-wrap { transform: scale(1.08) rotate(-4deg); }

.card-title {
  font-family: 'Playfair Display', serif;
  font-size: 1.2rem;
  font-weight: 700;
  color: var(--clinic-dark);
  margin-bottom: 8px;
}
.card-desc {
  font-size: 0.88rem;
  color: var(--clinic-muted);
  line-height: 1.65;
  margin-bottom: 14px;
}
.card-features {
  list-style: none;
  padding: 0; margin: 0 0 4px;
  display: flex; flex-direction: column; gap: 6px;
}
.card-features li {
  display: flex;
  align-items: center;
  gap: 6px;
  font-size: 0.83rem;
  color: var(--clinic-text);
  font-weight: 500;
}

.learn-more-btn {
  color: var(--clinic-primary) !important;
  font-weight: 600 !important;
  text-transform: none !important;
  letter-spacing: 0 !important;
  font-size: 0.88rem !important;
}
</style>