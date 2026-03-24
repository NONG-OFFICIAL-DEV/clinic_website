<template>
  <section id="appointment" class="appointment-section py-20" ref="sectionRef">
    <v-container style="max-width:1280px">
      <v-row align="stretch" class="ga-0">

        <!-- Left info panel -->
        <v-col cols="12" md="5" class="pr-md-8">
          <div class="info-panel anim-left" :class="{ visible: inView }">
            <div class="section-badge mb-4">Easy Booking</div>
            <h2 class="section-title-light text-h3 mb-4">
              Book Your Appointment in Minutes
            </h2>
            <p class="info-desc mb-8">
              Choose your specialist, pick a time slot, and get confirmed instantly. 
              No long waits on the phone — just simple, fast healthcare access.
            </p>

            <div class="steps-list">
              <div v-for="(step, i) in steps" :key="step.title" class="step-item">
                <div class="step-num">{{ i + 1 }}</div>
                <div>
                  <div class="step-title">{{ step.title }}</div>
                  <div class="step-desc">{{ step.desc }}</div>
                </div>
              </div>
            </div>

            <!-- Contact info -->
            <div class="contact-chips mt-8">
              <div class="chip">
                <v-icon icon="mdi-phone" size="18" color="var(--clinic-secondary)" />
                <span>+1 (800) 555-VITA</span>
              </div>
              <div class="chip">
                <v-icon icon="mdi-email-outline" size="18" color="var(--clinic-secondary)" />
                <span>hello@vitaclinic.com</span>
              </div>
            </div>
          </div>
        </v-col>

        <!-- Right form -->
        <v-col cols="12" md="7">
          <div class="form-card anim-right" :class="{ visible: inView }">
            <div class="form-header">
              <h3 class="form-title">Schedule a Visit</h3>
              <p class="form-subtitle">All fields are required</p>
            </div>

            <v-form ref="formRef" @submit.prevent="submitForm">
              <v-row>
                <v-col cols="12" sm="6">
                  <v-text-field
                    v-model="form.firstName"
                    label="First Name"
                    variant="outlined"
                    rounded="lg"
                    prepend-inner-icon="mdi-account-outline"
                    color="var(--clinic-primary)"
                    :rules="[v => !!v || 'Required']"
                    class="form-field"
                  />
                </v-col>
                <v-col cols="12" sm="6">
                  <v-text-field
                    v-model="form.lastName"
                    label="Last Name"
                    variant="outlined"
                    rounded="lg"
                    prepend-inner-icon="mdi-account-outline"
                    color="var(--clinic-primary)"
                    :rules="[v => !!v || 'Required']"
                    class="form-field"
                  />
                </v-col>
                <v-col cols="12" sm="6">
                  <v-text-field
                    v-model="form.email"
                    label="Email Address"
                    type="email"
                    variant="outlined"
                    rounded="lg"
                    prepend-inner-icon="mdi-email-outline"
                    color="var(--clinic-primary)"
                    :rules="[v => !!v || 'Required', v => /.+@.+\..+/.test(v) || 'Invalid email']"
                    class="form-field"
                  />
                </v-col>
                <v-col cols="12" sm="6">
                  <v-text-field
                    v-model="form.phone"
                    label="Phone Number"
                    variant="outlined"
                    rounded="lg"
                    prepend-inner-icon="mdi-phone-outline"
                    color="var(--clinic-primary)"
                    :rules="[v => !!v || 'Required']"
                    class="form-field"
                  />
                </v-col>
                <v-col cols="12" sm="6">
                  <v-select
                    v-model="form.department"
                    label="Department"
                    :items="departments"
                    variant="outlined"
                    rounded="lg"
                    prepend-inner-icon="mdi-medical-bag"
                    color="var(--clinic-primary)"
                    :rules="[v => !!v || 'Required']"
                    class="form-field"
                  />
                </v-col>
                <v-col cols="12" sm="6">
                  <v-text-field
                    v-model="form.date"
                    label="Preferred Date"
                    type="date"
                    variant="outlined"
                    rounded="lg"
                    prepend-inner-icon="mdi-calendar-outline"
                    color="var(--clinic-primary)"
                    :rules="[v => !!v || 'Required']"
                    class="form-field"
                  />
                </v-col>
                <v-col cols="12">
                  <v-select
                    v-model="form.time"
                    label="Preferred Time Slot"
                    :items="timeSlots"
                    variant="outlined"
                    rounded="lg"
                    prepend-inner-icon="mdi-clock-outline"
                    color="var(--clinic-primary)"
                    :rules="[v => !!v || 'Required']"
                    class="form-field"
                  />
                </v-col>
                <v-col cols="12">
                  <v-textarea
                    v-model="form.notes"
                    label="Additional Notes (Optional)"
                    variant="outlined"
                    rounded="lg"
                    prepend-inner-icon="mdi-note-text-outline"
                    color="var(--clinic-primary)"
                    rows="3"
                    no-resize
                    class="form-field"
                  />
                </v-col>
              </v-row>

              <v-btn
                type="submit"
                class="submit-btn w-100 mt-2"
                size="large"
                rounded="xl"
                :loading="submitting"
                prepend-icon="mdi-calendar-check"
              >
                Confirm Appointment
              </v-btn>
            </v-form>
          </div>
        </v-col>

      </v-row>
    </v-container>

    <!-- Success snackbar -->
    <v-snackbar v-model="successSnack" color="success" rounded="xl" :timeout="4000" location="top">
      <v-icon icon="mdi-check-circle" class="mr-2" />
      Appointment booked successfully! We'll confirm via email.
    </v-snackbar>
  </section>
</template>

<script setup>
import { ref, reactive, onMounted } from 'vue'

const sectionRef = ref(null)
const inView = ref(false)
const formRef = ref(null)
const submitting = ref(false)
const successSnack = ref(false)

const form = reactive({
  firstName: '', lastName: '', email: '', phone: '',
  department: '', date: '', time: '', notes: '',
})

const departments = [
  'General Medicine', 'Cardiology', 'Orthopedics',
  'Pediatrics', 'Neurology', 'Ophthalmology',
]

const timeSlots = [
  '08:00 AM – 09:00 AM', '09:00 AM – 10:00 AM', '10:00 AM – 11:00 AM',
  '11:00 AM – 12:00 PM', '02:00 PM – 03:00 PM', '03:00 PM – 04:00 PM',
  '04:00 PM – 05:00 PM',
]

const steps = [
  { title: 'Choose a Specialty',     desc: 'Select the medical department that fits your needs.' },
  { title: 'Pick a Time Slot',       desc: 'Browse available dates and book at your convenience.' },
  { title: 'Confirm & Get Ready',    desc: 'Receive instant email confirmation with all details.' },
]

async function submitForm() {
  const { valid } = await formRef.value.validate()
  if (!valid) return
  submitting.value = true
  await new Promise(r => setTimeout(r, 1600))
  submitting.value = false
  successSnack.value = true
  formRef.value.reset()
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
.appointment-section {
  background: linear-gradient(160deg, #f0faf8 0%, #fff 50%, #f0faf8 100%);
}

.section-badge {
  display: inline-block;
  background: var(--clinic-light);
  color: var(--clinic-primary);
  font-weight: 600; font-size: 0.82rem;
  letter-spacing: 0.1em; text-transform: uppercase;
  border-radius: 50px; padding: 6px 18px;
}

.info-panel {
  height: 100%;
  opacity: 0; transform: translateX(-30px);
  transition: all 0.7s ease;
}
.info-panel.visible { opacity: 1; transform: translateX(0); }

.section-title-light {
  font-family: 'Playfair Display', serif !important;
  font-weight: 700 !important;
  color: var(--clinic-dark) !important;
  line-height: 1.25 !important;
}
.info-desc { color: var(--clinic-muted); line-height: 1.75; font-size: 1rem; }

.steps-list { display: flex; flex-direction: column; gap: 20px; }
.step-item { display: flex; align-items: flex-start; gap: 18px; }
.step-num {
  min-width: 36px; height: 36px;
  background: linear-gradient(135deg, var(--clinic-primary), var(--clinic-secondary));
  color: white;
  border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  font-weight: 700; font-size: 0.88rem;
  box-shadow: 0 4px 14px rgba(10,110,97,0.3);
}
.step-title { font-weight: 700; color: var(--clinic-dark); font-size: 0.95rem; }
.step-desc  { font-size: 0.83rem; color: var(--clinic-muted); margin-top: 3px; }

.contact-chips { display: flex; flex-direction: column; gap: 12px; }
.chip {
  display: flex; align-items: center; gap: 12px;
  background: white;
  border-radius: 12px; padding: 12px 18px;
  box-shadow: 0 4px 16px rgba(10,110,97,0.08);
  font-size: 0.88rem; font-weight: 500; color: var(--clinic-dark);
}

/* Form card */
.form-card {
  background: white;
  border-radius: 28px;
  padding: 40px 36px;
  box-shadow: 0 8px 40px rgba(10,110,97,0.12);
  opacity: 0; transform: translateX(30px);
  transition: all 0.7s ease 0.15s;
}
.form-card.visible { opacity: 1; transform: translateX(0); }

.form-header { margin-bottom: 28px; }
.form-title {
  font-family: 'Playfair Display', serif;
  font-size: 1.5rem; font-weight: 700;
  color: var(--clinic-dark);
}
.form-subtitle { font-size: 0.83rem; color: var(--clinic-muted); margin-top: 4px; }

.form-field :deep(.v-field) { font-family: 'DM Sans', sans-serif; }

.submit-btn {
  background: linear-gradient(135deg, var(--clinic-primary), var(--clinic-secondary)) !important;
  color: white !important;
  font-weight: 700 !important;
  font-size: 1rem !important;
  text-transform: none !important;
  letter-spacing: 0 !important;
  box-shadow: 0 8px 28px rgba(10,110,97,0.35) !important;
  transition: transform 0.2s, box-shadow 0.2s !important;
}
.submit-btn:hover { transform: translateY(-3px); box-shadow: 0 14px 36px rgba(10,110,97,0.45) !important; }

.anim-right {
  opacity: 0; transform: translateX(30px);
  transition: all 0.7s ease 0.15s;
}
.anim-right.visible { opacity: 1; transform: translateX(0); }

@media (max-width: 960px) {
  .form-card { padding: 28px 20px; }
}
</style>