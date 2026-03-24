<template>
  <section id="contact" class="contact-section py-20" ref="sectionRef">
    <v-container style="max-width: 1280px">
      <div class="text-center mb-14">
        <div class="section-badge" :class="{ visible: inView }">
          Get In Touch
        </div>
        <h2
          class="section-title text-h3 mt-3 anim-title"
          :class="{ visible: inView }"
        >
          We're Here When You Need Us
        </h2>
        <p
          class="section-subtitle mt-4 mx-auto anim-sub"
          :class="{ visible: inView }"
          style="max-width: 480px"
        >
          Whether it's a question, emergency, or follow-up — our team is
          available around the clock.
        </p>
      </div>

      <v-row>
        <!-- Contact info cards -->
        <v-col
          v-for="(info, i) in contactInfo"
          :key="info.title"
          cols="12"
          sm="6"
          lg="3"
        >
          <div
            class="info-card"
            :class="{ visible: inView }"
            :style="{ transitionDelay: `${i * 0.12}s` }"
          >
            <div class="info-icon-wrap" :style="{ background: info.bg }">
              <v-icon :icon="info.icon" color="white" size="26" />
            </div>
            <div class="info-title">{{ info.title }}</div>
            <div v-for="line in info.lines" :key="line" class="info-line">
              {{ line }}
            </div>
          </div>
        </v-col>
      </v-row>

      <!-- Map placeholder -->
      <div class="map-card mt-12 anim-fade-up" :class="{ visible: inView }">
        <div class="map-inner">
          <div class="map-overlay-info">
            <div class="map-pin-icon">
              <v-icon icon="mdi-map-marker" color="white" size="28" />
            </div>
            <div class="map-address">
              <div class="map-clinic-name">VitaClinic Medical Center</div>
              <div class="map-addr-text">
                123 Healthcare Blvd, Suite 400
                <br />
                New York, NY 10001
              </div>
            </div>
            <v-btn
              class="directions-btn ml-auto"
              rounded="xl"
              prepend-icon="mdi-directions"
              href="https://maps.google.com"
              target="_blank"
            >
              Directions
            </v-btn>
          </div>
          <!-- Fake map grid -->
          <div class="map-container">
            <iframe
              width="100%"
              height="100%"
              style="border: 0"
              loading="lazy"
              allowfullscreen
              referrerpolicy="no-referrer-when-downgrade"
              src="https://www.google.com/maps?q=Phnom+Penh&output=embed"
            ></iframe>
          </div>
        </div>
      </div>
    </v-container>
  </section>
</template>

<script setup>
  import { ref, onMounted } from 'vue'

  const sectionRef = ref(null)
  const inView = ref(false)

  const contactInfo = [
    {
      title: 'Our Address',
      icon: 'mdi-map-marker-outline',
      bg: 'linear-gradient(135deg,#0a6e61,#12a090)',
      lines: ['123 Healthcare Blvd', 'Suite 400, New York, NY 10001']
    },
    {
      title: 'Phone',
      icon: 'mdi-phone-outline',
      bg: 'linear-gradient(135deg,#d72660,#f45d96)',
      lines: ['+1 (800) 555-VITA', '+1 (212) 555-8420']
    },
    {
      title: 'Email',
      icon: 'mdi-email-outline',
      bg: 'linear-gradient(135deg,#5b2fc9,#8a63d2)',
      lines: ['hello@vitaclinic.com', 'emergency@vitaclinic.com']
    },
    {
      title: 'Working Hours',
      icon: 'mdi-clock-outline',
      bg: 'linear-gradient(135deg,#e07b10,#f4a940)',
      lines: ['Mon–Fri: 7AM – 9PM', 'Sat–Sun: 8AM – 6PM']
    }
  ]

  function isRoad(n) {
    const row = Math.ceil(n / 10)
    const col = n % 10 || 10
    return row === 4 || row === 7 || col === 3 || col === 7
  }

  onMounted(() => {
    const obs = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) inView.value = true
      },
      { threshold: 0.1 }
    )
    if (sectionRef.value) obs.observe(sectionRef.value)
  })
</script>

<style scoped>
  .contact-section {
    background: linear-gradient(160deg, #fff 0%, #f0faf8 100%);
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
    opacity: 0;
    transform: translateY(16px);
    transition: all 0.6s ease;
  }
  .section-badge.visible {
    opacity: 1;
    transform: translateY(0);
  }
  .anim-title {
    opacity: 0;
    transform: translateY(24px);
    transition: all 0.7s ease 0.15s;
  }
  .anim-title.visible {
    opacity: 1;
    transform: translateY(0);
  }
  .anim-sub {
    opacity: 0;
    transform: translateY(20px);
    transition: all 0.7s ease 0.28s;
  }
  .anim-sub.visible {
    opacity: 1;
    transform: translateY(0);
  }

  /* Info cards */
  .info-card {
    background: white;
    border-radius: 20px;
    padding: 28px 24px;
    box-shadow: 0 4px 24px rgba(10, 110, 97, 0.08);
    border: 1px solid #e8f5f3;
    text-align: center;
    opacity: 0;
    transform: translateY(36px);
    transition:
      opacity 0.65s ease,
      transform 0.65s ease,
      box-shadow 0.3s ease;
    height: 100%;
  }
  .info-card.visible {
    opacity: 1;
    transform: translateY(0);
  }
  .info-card:hover {
    box-shadow: 0 16px 44px rgba(10, 110, 97, 0.14);
    transform: translateY(-6px) !important;
  }

  .info-icon-wrap {
    width: 58px;
    height: 58px;
    border-radius: 16px;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0 auto 16px;
    box-shadow: 0 6px 18px rgba(0, 0, 0, 0.15);
  }
  .info-title {
    font-family: 'Playfair Display', serif;
    font-size: 1.05rem;
    font-weight: 700;
    color: var(--clinic-dark);
    margin-bottom: 10px;
  }
  .info-line {
    font-size: 0.85rem;
    color: var(--clinic-muted);
    font-weight: 500;
    line-height: 1.8;
  }

  /* Map card */
  .map-card {
    border-radius: 24px;
    overflow: hidden;
    box-shadow: 0 8px 40px rgba(10, 110, 97, 0.12);
    opacity: 0;
    transform: translateY(30px);
    transition: all 0.7s ease 0.3s;
  }
  .map-card.visible {
    opacity: 1;
    transform: translateY(0);
  }

  .anim-fade-up {
    opacity: 0;
    transform: translateY(30px);
    transition: all 0.7s ease 0.3s;
  }
  .anim-fade-up.visible {
    opacity: 1;
    transform: translateY(0);
  }

  .map-inner {
    position: relative;
    height: 300px;
    background: #d0e8e3;
    overflow: hidden;
  }

  /* Fake grid map */
  .fake-map {
    display: grid;
    grid-template-columns: repeat(10, 1fr);
    height: 100%;
    opacity: 0.5;
  }
  .map-block {
    background: #c2dfd8;
    transition: background 0.3s;
  }
  .map-block.road {
    background: #e8f5f3;
  }

  .map-overlay-info {
    position: absolute;
    bottom: 20px;
    left: 20px;
    right: 20px;
    background: white;
    border-radius: 16px;
    padding: 18px 22px;
    display: flex;
    align-items: center;
    gap: 16px;
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.18);
    z-index: 2;
    flex-wrap: wrap;
  }
  .map-pin-icon {
    width: 48px;
    height: 48px;
    border-radius: 14px;
    background: linear-gradient(
      135deg,
      var(--clinic-primary),
      var(--clinic-secondary)
    );
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
  }
  .map-clinic-name {
    font-weight: 700;
    color: var(--clinic-dark);
    font-size: 0.95rem;
  }
  .map-addr-text {
    font-size: 0.8rem;
    color: var(--clinic-muted);
    margin-top: 2px;
  }

  .directions-btn {
    background: linear-gradient(
      135deg,
      var(--clinic-primary),
      var(--clinic-secondary)
    ) !important;
    color: white !important;
    font-weight: 600 !important;
    text-transform: none !important;
    letter-spacing: 0 !important;
    white-space: nowrap;
  }

  .map-container {
    width: 100%;
    height: 400px; /* adjust as you want */
    border-radius: 12px;
    overflow: hidden;
  }
</style>
