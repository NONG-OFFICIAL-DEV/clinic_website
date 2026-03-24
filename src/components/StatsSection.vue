<template>
  <section id="stats" class="stats-section" ref="sectionRef">
    <v-container style="max-width:1280px">
      <v-row align="center" class="py-16">

        <!-- Left text -->
        <v-col cols="12" md="5" class="pr-md-12">
          <div class="section-badge mb-4" :class="{ visible: inView }">Why Choose Us</div>
          <h2 class="section-title-light text-h3" :class="{ visible: inView, 'anim-left': true }">
            Trusted by Thousands of Patients
          </h2>
          <p class="stats-desc mt-4" :class="{ visible: inView, 'anim-left2': true }">
            Over 15 years of delivering compassionate, evidence-based healthcare 
            with measurable outcomes. Our patients' wellbeing is at the heart of everything we do.
          </p>
          <v-btn
            class="mt-6 learn-btn"
            size="large"
            rounded="xl"
            append-icon="mdi-arrow-right"
            :class="{ visible: inView, 'anim-left3': true }"
          >
            Our Story
          </v-btn>
        </v-col>

        <!-- Right stats grid -->
        <v-col cols="12" md="7">
          <v-row>
            <v-col
              v-for="(stat, i) in stats"
              :key="stat.label"
              cols="6"
            >
              <div
                class="stat-card"
                :class="{ visible: inView }"
                :style="{ transitionDelay: `${0.1 + i * 0.12}s` }"
              >
                <div class="stat-icon" :style="{ background: stat.bg }">
                  <v-icon :icon="stat.icon" color="white" size="26" />
                </div>
                <div class="stat-number">
                  <span class="counter">{{ inView ? stat.value : '0' }}</span>{{ stat.suffix }}
                </div>
                <div class="stat-label">{{ stat.label }}</div>
                <div class="stat-bar">
                  <div
                    class="stat-bar-fill"
                    :style="{ width: inView ? stat.pct + '%' : '0%', background: stat.color }"
                  />
                </div>
              </div>
            </v-col>
          </v-row>
        </v-col>

      </v-row>
    </v-container>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const sectionRef = ref(null)
const inView = ref(false)

const stats = [
  { label: 'Happy Patients',    value: '12K', suffix: '+', icon: 'mdi-account-heart',   bg: 'linear-gradient(135deg,#0a6e61,#12a090)', color: '#12a090', pct: 90 },
  { label: 'Specialist Doctors',value: '50',  suffix: '+', icon: 'mdi-doctor',          bg: 'linear-gradient(135deg,#d72660,#f45d96)', color: '#d72660', pct: 75 },
  { label: 'Years of Service',  value: '15',  suffix: '+', icon: 'mdi-medal-outline',   bg: 'linear-gradient(135deg,#e07b10,#f4a940)', color: '#f4a940', pct: 80 },
  { label: 'Treatments Done',   value: '98',  suffix: 'K+',icon: 'mdi-needle',          bg: 'linear-gradient(135deg,#5b2fc9,#8a63d2)', color: '#8a63d2', pct: 95 },
]

onMounted(() => {
  const obs = new IntersectionObserver(
    ([entry]) => { if (entry.isIntersecting) inView.value = true },
    { threshold: 0.15 }
  )
  if (sectionRef.value) obs.observe(sectionRef.value)
})
</script>

<style scoped>
.stats-section {
  background: linear-gradient(135deg, var(--clinic-dark) 0%, var(--clinic-primary) 100%);
  position: relative;
  overflow: hidden;
}
.stats-section::before {
  content: '';
  position: absolute; inset: 0;
  background: url("data:image/svg+xml,%3Csvg width='60' height='60' viewBox='0 0 60 60' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='none' fill-rule='evenodd'%3E%3Cg fill='%23ffffff' fill-opacity='0.04'%3E%3Cpath d='M36 34v-4h-2v4h-4v2h4v4h2v-4h4v-2h-4zm0-30V0h-2v4h-4v2h4v4h2V6h4V4h-4zM6 34v-4H4v4H0v2h4v4h2v-4h4v-2H6zM6 4V0H4v4H0v2h4v4h2V6h4V4H6z'/%3E%3C/g%3E%3C/g%3E%3C/svg%3E");
}

.section-badge {
  display: inline-block;
  background: rgba(255,255,255,0.15);
  color: rgba(255,255,255,0.9);
  font-weight: 600;
  font-size: 0.82rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  border-radius: 50px;
  padding: 6px 18px;
  opacity: 0; transform: translateY(16px);
  transition: all 0.6s ease;
}
.section-badge.visible { opacity: 1; transform: translateY(0); }

.section-title-light {
  font-family: 'Playfair Display', serif !important;
  font-weight: 700 !important;
  color: white !important;
  line-height: 1.25 !important;
}
.anim-left {
  opacity: 0; transform: translateX(-30px);
  transition: all 0.7s ease 0.15s;
}
.anim-left.visible { opacity: 1; transform: translateX(0); }
.anim-left2 {
  opacity: 0; transform: translateX(-30px);
  transition: all 0.7s ease 0.28s;
}
.anim-left2.visible { opacity: 1; transform: translateX(0); }
.anim-left3 {
  opacity: 0; transform: translateX(-30px);
  transition: all 0.7s ease 0.4s;
}
.anim-left3.visible { opacity: 1; transform: translateX(0); }

.stats-desc { color: rgba(255,255,255,0.75); font-size: 1rem; line-height: 1.75; }

.learn-btn {
  background: white !important;
  color: var(--clinic-primary) !important;
  font-weight: 600 !important;
  text-transform: none !important;
  letter-spacing: 0 !important;
}

/* Stat card */
.stat-card {
  background: rgba(255,255,255,0.1);
  backdrop-filter: blur(12px);
  border: 1px solid rgba(255,255,255,0.18);
  border-radius: 20px;
  padding: 28px 24px;
  opacity: 0; transform: translateY(30px);
  transition: opacity 0.6s ease, transform 0.6s ease, background 0.3s ease;
  margin-bottom: 16px;
}
.stat-card.visible { opacity: 1; transform: translateY(0); }
.stat-card:hover { background: rgba(255,255,255,0.16); }

.stat-icon {
  width: 50px; height: 50px;
  border-radius: 14px;
  display: flex; align-items: center; justify-content: center;
  margin-bottom: 16px;
  box-shadow: 0 6px 18px rgba(0,0,0,0.2);
}
.stat-number {
  font-family: 'Playfair Display', serif;
  font-size: 2rem;
  font-weight: 700;
  color: white;
  line-height: 1;
  margin-bottom: 6px;
}
.stat-label {
  font-size: 0.83rem;
  color: rgba(255,255,255,0.65);
  font-weight: 500;
  margin-bottom: 14px;
}
.stat-bar {
  height: 4px;
  background: rgba(255,255,255,0.15);
  border-radius: 4px;
  overflow: hidden;
}
.stat-bar-fill {
  height: 100%;
  border-radius: 4px;
  transition: width 1.4s cubic-bezier(0.4,0,0.2,1);
}
</style>