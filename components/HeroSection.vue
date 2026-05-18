<template>
  <section class="hero-section relative text-white overflow-hidden">
    <div class="absolute inset-0 -z-10 bg-black/70"></div>

    <!-- Navbar -->
    <div class="border-b border-white/10 bg-black/60 backdrop-blur-sm">
      <div class="max-w-7xl mx-auto px-6 py-3 flex justify-center">
        <img :src="logoPath" alt="Convertixz" class="h-6 md:h-7 object-contain" />
      </div>
    </div>

    <div class="max-w-7xl mx-auto px-6 py-20 md:py-24 text-center">
      <h1 class="text-white font-serif leading-tight drop-shadow-lg text-4xl sm:text-6xl md:text-7xl mb-6">
        More Conversations. More Clients. More Revenue.
      </h1>

      <p class="text-amber-200 text-lg md:text-xl mb-8 max-w-2xl mx-auto">
        Convertixz helps businesses generate qualified leads through strategic outreach, high-converting funnels, and performance-driven growth systems designed to scale revenue consistently.
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
        Helping agencies build predictable pipelines with smarter acquisition systems.
      </p>
    </div>

    <div class="absolute inset-x-0 bottom-0 h-24 bg-gradient-to-t from-black/80 to-transparent pointer-events-none"></div>
  </section>
</template>

<script setup lang="ts">
import { computed } from 'vue'

const emit = defineEmits<{
  (e: 'open-form'): void
}>()

const logoPath = '/typoLogo.jpeg'

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
.hero-section {
  background: linear-gradient(rgba(0, 0, 0, 0.85), rgba(0, 0, 0, 0.85)), url('/heroBg.jpg');
  background-size: cover;
  background-position: center;
}
</style>
