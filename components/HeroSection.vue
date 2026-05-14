<template>
  <section class="relative bg-black text-white overflow-hidden">
    <div class="hero-bg absolute inset-0 -z-10"></div>

    <!-- Navbar -->
    <div class="border-b border-white/10 bg-black/60 backdrop-blur-sm">
      <div class="max-w-7xl mx-auto px-6 py-3 flex justify-center">
        <img :src="logoPath" alt="Convertix" class="h-6 md:h-7 object-contain" />
      </div>
    </div>

    <div class="max-w-7xl mx-auto px-6 py-20 md:py-24 text-center">
      <h1 class="text-white font-serif leading-tight drop-shadow-lg text-4xl sm:text-6xl md:text-7xl mb-6">
        More Conversations. More Clients. More Revenue.
      </h1>

      <p class="text-amber-200 text-lg md:text-xl mb-8 max-w-2xl mx-auto">
        Convertix helps businesses generate qualified leads through strategic outreach, high-converting funnels, and performance-driven growth systems designed to scale revenue consistently.
      </p>

      <div class="flex justify-center gap-4 mb-12">
        <button
          type="button"
          class="inline-block px-6 py-3 rounded-md font-semibold shadow-md"
          :style="primaryBtnStyle"
          @click="openModal"
        >
          Book a Strategy Call
        </button>
        <button
          type="button"
          class="inline-block px-6 py-3 rounded-md font-semibold bg-white text-black"
          @click="openModal"
        >
          Get Started
        </button>
      </div>

      <p class="text-sm text-white/75 max-w-2xl mx-auto mb-8">
        Helping brands build predictable pipelines with smarter acquisition systems.
      </p>

      <div class="mt-10">
        <p class="text-sm text-amber-100 mb-4">Trusted by companies like:</p>
        <div class="relative overflow-hidden border border-white/10 rounded-xl bg-white/5 py-4">
          <div class="edge-fade-left absolute inset-y-0 left-0 w-16 md:w-24 z-10 pointer-events-none"></div>
          <div class="edge-fade-right absolute inset-y-0 right-0 w-16 md:w-24 z-10 pointer-events-none"></div>

          <div class="marquee-track">
            <div class="marquee-row">
              <span v-for="company in companies" :key="`a-${company}`" class="company-pill">{{ company }}</span>
            </div>
            <div class="marquee-row" aria-hidden="true">
              <span v-for="company in companies" :key="`b-${company}`" class="company-pill">{{ company }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="absolute inset-x-0 bottom-0 h-24 bg-gradient-to-t from-black/80 to-transparent pointer-events-none"></div>
  </section>
</template>

<script setup lang="ts">
import { computed } from 'vue'

const emit = defineEmits<{
  (e: 'open-form'): void
}>()

const logoPath = '/typoLogo.jpg'
const companies = ['DREW', 'SOFI', 'TURBOTAX', 'VENMO', 'FITBODY', 'HOSTINGER', 'BUILT', 'DAVE RAMSEY']

// inline color from provided palette (pale-amber 500)
const primaryColor = '#c8cb34'

const primaryBtnStyle = computed(() => ({
  background: `linear-gradient(180deg, ${primaryColor}, ${darken(primaryColor, -20)})`,
  color: '#000',
  boxShadow: '0 8px 24px rgba(200,203,52,0.18)'
}))

function darken(hex: string, percent: number) {
  // simple darken by shifting rgb channels; percent negative to darken
  const num = parseInt(hex.replace('#',''),16)
  let r = (num >> 16) + percent
  let g = ((num >> 8) & 0x00FF) + percent
  let b = (num & 0x0000FF) + percent
  r = Math.max(Math.min(255, r), 0)
  g = Math.max(Math.min(255, g), 0)
  b = Math.max(Math.min(255, b), 0)
  return `#${(r<<16 | g<<8 | b).toString(16).padStart(6,'0')}`
}

function openModal() {
  emit('open-form')
}
</script>

<style scoped>
.hero-bg {
  background: radial-gradient(ellipse at bottom, rgba(200,203,52,0.08) 0%, rgba(0,0,0,0.65) 40%), linear-gradient(180deg, #000 0%, #0b0b0b 100%);
  background-size: cover;
}

.marquee-track {
  width: max-content;
  display: flex;
  align-items: center;
  animation: marquee 24s linear infinite;
}

.marquee-row {
  display: flex;
  align-items: center;
  gap: 1.25rem;
  padding-inline: 0.625rem;
}

.company-pill {
  color: rgba(255, 255, 255, 0.82);
  letter-spacing: 0.08em;
  font-size: 0.78rem;
  border: 1px solid rgba(255, 255, 255, 0.16);
  padding: 0.45rem 0.8rem;
  border-radius: 9999px;
  background: rgba(255, 255, 255, 0.04);
}

.edge-fade-left {
  background: linear-gradient(90deg, rgba(0, 0, 0, 0.92), rgba(0, 0, 0, 0));
}

.edge-fade-right {
  background: linear-gradient(270deg, rgba(0, 0, 0, 0.92), rgba(0, 0, 0, 0));
}

@keyframes marquee {
  0% {
    transform: translateX(0%);
  }
  100% {
    transform: translateX(-50%);
  }
}
</style>
