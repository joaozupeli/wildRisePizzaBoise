<script setup>
import { reactive, ref } from 'vue'
import { clinic } from '../../data/clinic'
import { specialties } from '../../data/specialties'
import { useReveal, useSplitReveal } from '../../composables/useMotion'
import Icon from '../ui/Icon.vue'

const section = ref(null)
const title = ref(null)

useSplitReveal(title)
useReveal(section, { selector: '[data-anim]', y: 24, stagger: 0.06 })

const form = reactive({
  name: '',
  phone: '',
  specialty: '',
  message: '',
})

function onSubmit() {
  window.open(clinic.orderUrl, '_blank', 'noopener,noreferrer')
}
</script>

<template>
  <section id="contato" ref="section" class="section contact">
    <div class="container">
      <div class="contact__head">
        <div>
          <p class="eyebrow">05 — Order</p>
          <h2 ref="title" class="contact__title display">
            This week's <em>pickup window</em>
          </h2>
        </div>
        <p data-anim class="lead contact__lead">
          Checkout lives on Hotplate. Follow Instagram for drop day, kitchen-window hours, and delivery notes.
        </p>
      </div>

      <div class="contact__grid">
        <div class="contact__info">
          <div data-anim class="info">
            <p class="mono info__label">Area</p>
            <p class="info__value">
              {{ clinic.address.street }}<br />
              {{ clinic.address.neighborhood }}<br />
              {{ clinic.address.city }}, {{ clinic.address.state }}
            </p>
          </div>

          <div data-anim class="info">
            <p class="mono info__label">Order &amp; updates</p>
            <p class="info__value">
              <a :href="clinic.instagramUrl" target="_blank" rel="noopener noreferrer">{{
                clinic.phone
              }}</a><br />
              <a :href="clinic.orderUrl" target="_blank" rel="noopener noreferrer">{{
                clinic.email
              }}</a>
            </p>
          </div>

          <div data-anim class="info">
            <p class="mono info__label">Rhythm</p>
            <p v-for="item in clinic.hours" :key="item.days" class="info__value info__row">
              <span>{{ item.days }}</span>
              <span>{{ item.time }}</span>
            </p>
          </div>

          <div data-anim class="info">
            <p class="mono info__label">Good to know</p>
            <ul class="info__tags">
              <li v-for="item in clinic.insurance" :key="item" class="mono">{{ item }}</li>
            </ul>
          </div>
        </div>

        <form data-anim class="form" @submit.prevent="onSubmit">
          <label class="field">
            <span class="mono">Your name</span>
            <input v-model="form.name" type="text" autocomplete="name" required placeholder="What should we call you" />
          </label>

          <label class="field">
            <span class="mono">Neighborhood</span>
            <input v-model="form.phone" type="text" placeholder="Boise area (optional)" />
          </label>

          <label class="field">
            <span class="mono">Kit interest</span>
            <select v-model="form.specialty" required>
              <option value="" disabled>Pick a kit</option>
              <option v-for="item in specialties" :key="item.id" :value="item.id">
                {{ item.title }}
              </option>
            </select>
          </label>

          <label class="field">
            <span class="mono">Note</span>
            <textarea v-model="form.message" rows="3" placeholder="Pickup, delivery, or a question about this week" />
          </label>

          <div class="form__actions">
            <button class="btn btn--solid form__submit" type="submit">
              <Icon name="bag" :size="16" />
              Order on Hotplate
            </button>
            <a class="link" :href="clinic.instagramUrl" target="_blank" rel="noopener noreferrer">
              <Icon name="instagram" :size="14" />
              Instagram
            </a>
          </div>
        </form>
      </div>
    </div>

    <div data-anim class="contact__map">
      <iframe
        :title="`Map of ${clinic.address.city}, ${clinic.address.state}`"
        :src="clinic.address.mapEmbedUrl"
        loading="lazy"
        referrerpolicy="no-referrer-when-downgrade"
        allowfullscreen
      />
    </div>
  </section>
</template>

<style scoped>
.contact {
  background: var(--paper-2);
  padding-bottom: 0;
}

.contact__head {
  display: grid;
  gap: 1.75rem;
  padding-bottom: clamp(2.5rem, 6vw, 4rem);
}

.contact__title {
  margin-top: 1.25rem;
  font-size: var(--display-md);
  max-width: 14ch;
}

.contact__lead {
  align-self: end;
}

.contact__grid {
  display: grid;
  gap: 3rem;
}

.info {
  padding-block: 1.25rem;
  border-top: 1px solid var(--line);
}

.info:last-child {
  border-bottom: 1px solid var(--line);
}

.info__label {
  color: var(--fg-faint);
  margin-bottom: 0.6rem;
}

.info__value {
  font-size: var(--text-base);
  line-height: 1.6;
}

.info__value a:hover {
  color: var(--clay);
}

.info__row {
  display: flex;
  justify-content: space-between;
  gap: 1rem;
  color: var(--fg-soft);
}

.info__tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.4rem;
}

.info__tags li {
  padding: 0.35rem 0.7rem;
  border: 1px solid var(--line);
  border-radius: 999px;
  color: var(--fg-soft);
}

.form {
  display: grid;
  gap: 1.75rem;
  align-content: start;
}

.field {
  display: grid;
  gap: 0.5rem;
}

.field > .mono {
  color: var(--fg-faint);
}

.field input,
.field select,
.field textarea {
  width: 100%;
  padding: 0.65rem 0;
  border: 0;
  border-bottom: 1px solid var(--line);
  border-radius: 0;
  background: transparent;
  font-family: var(--font-display);
  font-size: 1.35rem;
  color: var(--fg);
  transition: border-color 0.4s var(--ease);
}

.field textarea {
  font-family: var(--font-sans);
  font-size: var(--text-base);
  resize: vertical;
}

.field input::placeholder,
.field textarea::placeholder {
  color: var(--fg-faint);
  font-family: var(--font-sans);
  font-size: var(--text-base);
}

.field input:focus,
.field select:focus,
.field textarea:focus {
  outline: none;
  border-bottom-color: var(--clay);
}

.form__actions {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 1.25rem;
}

.form__submit {
  justify-self: start;
}

.contact__map {
  margin-top: clamp(3.5rem, 8vw, 6rem);
  aspect-ratio: 16 / 9;
  max-height: 30rem;
  background: var(--paper-3);
}

.contact__map iframe {
  width: 100%;
  height: 100%;
  border: 0;
  display: block;
  filter: grayscale(1) contrast(1.05);
  transition: filter 0.6s var(--ease);
}

.contact__map:hover iframe {
  filter: grayscale(0);
}

@media (min-width: 900px) {
  .contact__head {
    grid-template-columns: 1.3fr 0.7fr;
    gap: 3rem;
  }

  .contact__grid {
    grid-template-columns: 1fr 1fr;
    gap: 5rem;
  }
}
</style>
