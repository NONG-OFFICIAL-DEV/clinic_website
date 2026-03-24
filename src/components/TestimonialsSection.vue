<template>
  <section id="testimonials" class="testimonials-section py-20" ref="sectionRef">
    <v-container style="max-width:1280px">
      <div class="text-center mb-14">
        <div class="section-badge" :class="{ visible: inView }">Patient Stories</div>
        <h2 class="section-title text-h3 mt-3 anim-title" :class="{ visible: inView }">
          What Our Patients Say
        </h2>
        <p class="section-subtitle mt-4 mx-auto anim-sub" :class="{ visible: inView }" style="max-width:480px">
          Real experiences from real people who trusted us with their health.
        </p>
      </div>

      <!-- Testimonials -->
      <v-row>
        <v-col
          v-for="(t, i) in testimonials"
          :key="t.name"
          cols="12" md="4"
        >
          <div
            class="testimonial-card"
            :class="{ visible: inView }"
            :style="{ transitionDelay: `${i * 0.14}s` }"
          >
            <!-- Quote icon -->
            <div class="quote-mark">"</div>

            <!-- Stars -->
            <div class="stars-row mb-4">
              <v-icon
                v-for="n in 5"
                :key="n"
                icon="mdi-star"
                :color="n <= t.rating ? '#f4a940' : '#ddd'"
                size="18"
              />
            </div>

            <p class="testimonial-text">{{ t.text }}</p>

            <!-- Author -->
            <div class="author-row mt-6">
              <img :src="t.avatar" :alt="t.name" class="author-avatar" />
              <div>
                <div class="author-name">{{ t.name }}</div>
                <div class="author-role">{{ t.role }}</div>
              </div>
              <div class="service-tag ml-auto">{{ t.service }}</div>
            </div>
          </div>
        </v-col>
      </v-row>

      <!-- Overall rating bar -->
      <div class="rating-summary mt-12 anim-fade-up" :class="{ visible: inView }">
        <div class="rating-overall">
          <div class="rating-number">4.9</div>
          <div>
            <div class="stars-row mb-1">
              <v-icon v-for="n in 5" :key="n" icon="mdi-star" color="#f4a940" size="22" />
            </div>
            <div class="rating-label">Overall Patient Rating</div>
          </div>
        </div>
        <div class="rating-bars">
          <div v-for="bar in ratingBars" :key="bar.stars" class="rating-bar-row">
            <span class="bar-label">{{ bar.stars }}★</span>
            <div class="bar-track">
              <div class="bar-fill" :style="{ width: inView ? bar.pct + '%' : '0%' }" />
            </div>
            <span class="bar-pct">{{ bar.pct }}%</span>
          </div>
        </div>
        <div class="rating-count">
          <v-icon icon="mdi-account-group" color="var(--clinic-secondary)" />
          <span>Based on <strong>3,842</strong> verified reviews</span>
        </div>
      </div>
    </v-container>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const sectionRef = ref(null)
const inView = ref(false)

const testimonials = [
  {
    name: 'Amanda Torres',
    role: 'Recovered Patient',
    service: 'Cardiology',
    rating: 5,
    avatar: 'https://images.unsplash.com/photo-1494790108377-be9c29b29330?w=100&q=80',
    text: 'Dr. Mitchell saved my life. After my heart attack scare, the cardiology team responded instantly. The care I received was extraordinary — professional, warm, and thorough.',
  },
  {
    name: 'Robert Chen',
    role: 'Sports Athlete',
    service: 'Orthopedics',
    rating: 5,
    avatar: 'https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=100&q=80',
    text: 'I was back on the field 8 weeks after my knee surgery — far ahead of schedule. Dr. Hartmann and his team provided a recovery plan that actually worked for my lifestyle.',
  },
  {
    name: 'Fatima Al-Rashid',
    role: 'Parent',
    service: 'Pediatrics',
    rating: 5,
    avatar: 'https://images.unsplash.com/photo-1438761681033-6461ffad8d80?w=100&q=80',
    text: 'Taking my two kids to VitaClinic is always a calm experience. Dr. Sharma is amazing with children — patient, gentle, and so knowledgeable. Highly recommend!',
  },
]

const ratingBars = [
  { stars: 5, pct: 82 },
  { stars: 4, pct: 11 },
  { stars: 3, pct: 5  },
  { stars: 2, pct: 1  },
  { stars: 1, pct: 1  },
]

onMounted(() => {
  const obs = new IntersectionObserver(
    ([entry]) => { if (entry.isIntersecting) inView.value = true },
    { threshold: 0.1 }
  )
  if (sectionRef.value) obs.observe(sectionRef.value)
})
</script>

<style scoped>
.testimonials-section { background: #fff; }

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
.anim-sub   { opacity: 0; transform: translateY(20px); transition: all 0.7s ease 0.28s; }
.anim-sub.visible   { opacity: 1; transform: translateY(0); }

/* Testimonial card */
.testimonial-card {
  background: #fff;
  border: 1px solid #e8f5f3;
  border-radius: 24px;
  padding: 36px 28px 28px;
  box-shadow: 0 4px 24px rgba(10,110,97,0.07);
  position: relative;
  overflow: hidden;
  opacity: 0; transform: translateY(40px);
  transition: opacity 0.65s ease, transform 0.65s ease, box-shadow 0.3s ease;
  height: 100%;
}
.testimonial-card.visible { opacity: 1; transform: translateY(0); }
.testimonial-card:hover { box-shadow: 0 20px 50px rgba(10,110,97,0.14); transform: translateY(-6px) !important; }

.quote-mark {
  position: absolute;
  top: 16px; right: 24px;
  font-family: 'Playfair Display', serif;
  font-size: 5rem;
  line-height: 1;
  color: var(--clinic-light);
  font-weight: 700;
  user-select: none;
}

.stars-row { display: flex; gap: 2px; }

.testimonial-text {
  font-size: 0.93rem;
  line-height: 1.75;
  color: var(--clinic-muted);
  font-style: italic;
}

.author-row { display: flex; align-items: center; gap: 14px; }
.author-avatar {
  width: 46px; height: 46px;
  border-radius: 50%;
  object-fit: cover;
  border: 2px solid var(--clinic-light);
}
.author-name { font-weight: 700; color: var(--clinic-dark); font-size: 0.92rem; }
.author-role { font-size: 0.78rem; color: var(--clinic-muted); }
.service-tag {
  background: var(--clinic-light);
  color: var(--clinic-primary);
  border-radius: 50px;
  padding: 4px 12px;
  font-size: 0.72rem;
  font-weight: 600;
  white-space: nowrap;
}

/* Rating summary */
.rating-summary {
  background: linear-gradient(135deg, #f0faf8, #e0f4f0);
  border-radius: 24px;
  padding: 36px 40px;
  display: flex;
  align-items: center;
  gap: 48px;
  flex-wrap: wrap;
  opacity: 0; transform: translateY(30px);
  transition: all 0.7s ease 0.3s;
}
.rating-summary.visible { opacity: 1; transform: translateY(0); }

.rating-overall { display: flex; align-items: center; gap: 20px; }
.rating-number {
  font-family: 'Playfair Display', serif;
  font-size: 4rem;
  font-weight: 700;
  color: var(--clinic-dark);
  line-height: 1;
}
.rating-label { font-size: 0.83rem; color: var(--clinic-muted); font-weight: 500; }

.rating-bars { flex: 1; min-width: 200px; display: flex; flex-direction: column; gap: 8px; }
.rating-bar-row { display: flex; align-items: center; gap: 10px; }
.bar-label { font-size: 0.8rem; color: var(--clinic-muted); width: 20px; text-align: right; }
.bar-track {
  flex: 1;
  height: 8px;
  background: rgba(10,110,97,0.12);
  border-radius: 8px;
  overflow: hidden;
}
.bar-fill {
  height: 100%;
  background: linear-gradient(90deg, var(--clinic-primary), var(--clinic-secondary));
  border-radius: 8px;
  transition: width 1.2s cubic-bezier(0.4,0,0.2,1) 0.5s;
}
.bar-pct { font-size: 0.78rem; color: var(--clinic-muted); width: 32px; }

.rating-count {
  display: flex; align-items: center; gap: 8px;
  font-size: 0.88rem; color: var(--clinic-muted);
}
</style>