<template>
  <section id="doctors" class="doctors-section py-20" ref="sectionRef">
    <v-container style="max-width:1280px">
      <div class="text-center mb-14">
        <div class="section-badge" :class="{ visible: inView }">Meet the Team</div>
        <h2 class="section-title text-h3 mt-3" :class="{ visible: inView, 'anim-title': true }">
          Our Expert Doctors
        </h2>
        <p class="section-subtitle mt-4 mx-auto" :class="{ visible: inView, 'anim-sub': true }" style="max-width:500px">
          Board-certified physicians with decades of combined experience, committed to your wellbeing.
        </p>
      </div>

      <v-row>
        <v-col
          v-for="(doc, i) in doctors"
          :key="doc.name"
          cols="12" sm="6" lg="3"
        >
          <div
            class="doctor-card"
            :class="{ visible: inView }"
            :style="{ transitionDelay: `${i * 0.12}s` }"
          >
            <!-- Photo -->
            <div class="doctor-photo-wrap">
              <img :src="doc.photo" :alt="doc.name" class="doctor-photo" />
              <div class="photo-overlay">
                <div class="doctor-socials">
                  <v-btn
                    v-for="s in socials"
                    :key="s.icon"
                    :icon="s.icon"
                    variant="flat"
                    color="white"
                    size="small"
                    rounded
                    class="social-btn"
                  />
                </div>
              </div>
              <div class="availability-badge">
                <span class="avail-dot" />
                Available Today
              </div>
            </div>

            <!-- Info -->
            <div class="doctor-info">
              <div class="doctor-name">{{ doc.name }}</div>
              <div class="doctor-specialty">{{ doc.specialty }}</div>
              <div class="doctor-meta">
                <span><v-icon icon="mdi-school-outline" size="14" /> {{ doc.exp }} yrs exp.</span>
                <span>
                  <v-icon icon="mdi-star" size="14" color="#f4a940" />
                  {{ doc.rating }}
                </span>
              </div>
              <v-btn
                variant="outlined"
                rounded="lg"
                class="book-btn w-100 mt-3"
                prepend-icon="mdi-calendar-plus"
                @click="scrollTo('appointment')"
              >
                Book Session
              </v-btn>
            </div>
          </div>
        </v-col>
      </v-row>
    </v-container>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const sectionRef = ref(null)
const inView = ref(false)

const socials = [
  { icon: 'mdi-linkedin' },
  { icon: 'mdi-twitter' },
  { icon: 'mdi-email-outline' },
]

const doctors = [
  {
    name: 'Dr. Sarah Mitchell',
    specialty: 'Chief Cardiologist',
    photo: 'https://images.unsplash.com/photo-1559839734-2b71ea197ec2?w=400&q=80',
    exp: 18, rating: '4.9',
  },
  {
    name: 'Dr. James Okonkwo',
    specialty: 'Neurologist',
    photo: 'https://images.unsplash.com/photo-1612349317150-e413f6a5b16d?w=400&q=80',
    exp: 14, rating: '4.8',
  },
  {
    name: 'Dr. Priya Sharma',
    specialty: 'Pediatrician',
    photo: 'https://images.unsplash.com/photo-1594824476967-48c8b964273f?w=400&q=80',
    exp: 11, rating: '5.0',
  },
  {
    name: 'Dr. Leon Hartmann',
    specialty: 'Orthopedic Surgeon',
    photo: 'https://images.unsplash.com/photo-1622253692010-333f2da6031d?w=400&q=80',
    exp: 22, rating: '4.9',
  },
]

function scrollTo(id) {
  const el = document.getElementById(id)
  if (el) el.scrollIntoView({ behavior: 'smooth' })
}

onMounted(() => {
  const obs = new IntersectionObserver(
    ([entry]) => { if (entry.isIntersecting) inView.value = true },
    { threshold: 0.1 }
  )
  if (sectionRef.value) obs.observe(sectionRef.value)
})
</script>

<style scoped>
.doctors-section {
  background: linear-gradient(160deg, #f0faf8 0%, #fff 60%, #f0faf8 100%);
}

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
  opacity: 0; transform: translateY(16px);
  transition: all 0.6s ease;
}
.section-badge.visible { opacity: 1; transform: translateY(0); }

.anim-title { opacity: 0; transform: translateY(24px); transition: all 0.7s ease 0.15s; }
.anim-title.visible { opacity: 1; transform: translateY(0); }
.anim-sub   { opacity: 0; transform: translateY(20px); transition: all 0.7s ease 0.30s; }
.anim-sub.visible   { opacity: 1; transform: translateY(0); }

/* Doctor card */
.doctor-card {
  background: white;
  border-radius: 24px;
  overflow: hidden;
  box-shadow: 0 4px 24px rgba(10,110,97,0.08);
  opacity: 0; transform: translateY(40px);
  transition: opacity 0.65s ease, transform 0.65s ease, box-shadow 0.3s ease;
  cursor: pointer;
  height: 100%;
}
.doctor-card.visible { opacity: 1; transform: translateY(0); }
.doctor-card:hover { box-shadow: 0 24px 56px rgba(10,110,97,0.18); transform: translateY(-8px) !important; }

.doctor-photo-wrap {
  position: relative;
  overflow: hidden;
  height: 260px;
}
.doctor-photo {
  width: 100%; height: 100%;
  object-fit: cover;
  display: block;
  transition: transform 0.5s ease;
}
.doctor-card:hover .doctor-photo { transform: scale(1.06); }

.photo-overlay {
  position: absolute; inset: 0;
  background: rgba(6,46,41,0.55);
  display: flex; align-items: flex-end; justify-content: center;
  padding-bottom: 20px;
  opacity: 0;
  transition: opacity 0.3s ease;
}
.doctor-card:hover .photo-overlay { opacity: 1; }
.doctor-socials { display: flex; gap: 8px; }
.social-btn { opacity: 0.9; }
.social-btn:hover { opacity: 1; }

.availability-badge {
  position: absolute;
  top: 14px; left: 14px;
  background: white;
  border-radius: 50px;
  padding: 5px 12px;
  font-size: 0.75rem;
  font-weight: 600;
  color: var(--clinic-primary);
  display: flex; align-items: center; gap: 6px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}
.avail-dot {
  width: 8px; height: 8px;
  border-radius: 50%;
  background: #22c55e;
  animation: pulse-ring 2s infinite;
}

.doctor-info { padding: 20px; }
.doctor-name {
  font-family: 'Playfair Display', serif;
  font-size: 1.1rem;
  font-weight: 700;
  color: var(--clinic-dark);
}
.doctor-specialty {
  font-size: 0.83rem;
  color: var(--clinic-secondary);
  font-weight: 600;
  margin: 4px 0 12px;
}
.doctor-meta {
  display: flex;
  gap: 16px;
  font-size: 0.8rem;
  color: var(--clinic-muted);
  font-weight: 500;
}
.doctor-meta span { display: flex; align-items: center; gap: 4px; }

.book-btn {
  color: var(--clinic-primary) !important;
  border-color: var(--clinic-primary) !important;
  font-weight: 600 !important;
  text-transform: none !important;
  letter-spacing: 0 !important;
  transition: background 0.2s, color 0.2s !important;
}
.book-btn:hover {
  background: var(--clinic-primary) !important;
  color: white !important;
}
</style>