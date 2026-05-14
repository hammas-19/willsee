<template>
  <Teleport to="body">
    <div v-if="open" class="fixed inset-0 z-50 flex items-center justify-center px-4" @keydown.esc="closeModal">
      <button
        aria-label="Close modal overlay"
        class="absolute inset-0 bg-black/70 backdrop-blur-sm"
        type="button"
        @click="closeModal"
      ></button>

      <div class="relative z-10 w-full max-w-xl rounded-2xl border border-white/10 bg-[#111111] p-6 md:p-8 text-white shadow-2xl">
        <div class="mb-6 flex items-start justify-between gap-4">
          <div>
            <p class="text-xs uppercase tracking-[0.18em] text-[#c8cb34]">Convertix</p>
            <h3 class="mt-2 text-2xl md:text-3xl font-serif">Book a Strategy Call</h3>
            <p class="mt-2 text-sm text-white/70">Share a few details and our team will reach out shortly.</p>
          </div>
          <button
            aria-label="Close modal"
            class="rounded-md border border-white/20 px-3 py-1 text-sm text-white/80 hover:bg-white/10"
            type="button"
            @click="closeModal"
          >
            Close
          </button>
        </div>

        <form class="space-y-4" @submit.prevent="handleSubmit">
          <div class="grid gap-4 md:grid-cols-2">
            <label class="block text-sm">
              <span class="mb-1 block text-white/80">Full Name</span>
              <input
                v-model="form.fullName"
                required
                class="w-full rounded-md border border-white/20 bg-black/40 px-3 py-2 text-white outline-none focus:border-[#c8cb34]"
                type="text"
                placeholder="John Carter"
              />
            </label>

            <label class="block text-sm">
              <span class="mb-1 block text-white/80">Work Email</span>
              <input
                v-model="form.email"
                required
                class="w-full rounded-md border border-white/20 bg-black/40 px-3 py-2 text-white outline-none focus:border-[#c8cb34]"
                type="email"
                placeholder="you@company.com"
              />
            </label>
          </div>

          <div class="grid gap-4 md:grid-cols-2">
            <label class="block text-sm">
              <span class="mb-1 block text-white/80">Company</span>
              <input
                v-model="form.company"
                class="w-full rounded-md border border-white/20 bg-black/40 px-3 py-2 text-white outline-none focus:border-[#c8cb34]"
                type="text"
                placeholder="Acme Inc."
              />
            </label>

            <label class="block text-sm">
              <span class="mb-1 block text-white/80">Monthly Lead Goal</span>
              <input
                v-model="form.leadGoal"
                class="w-full rounded-md border border-white/20 bg-black/40 px-3 py-2 text-white outline-none focus:border-[#c8cb34]"
                type="text"
                placeholder="50+ qualified leads"
              />
            </label>
          </div>

          <label class="block text-sm">
            <span class="mb-1 block text-white/80">How can we help?</span>
            <textarea
              v-model="form.message"
              rows="4"
              class="w-full rounded-md border border-white/20 bg-black/40 px-3 py-2 text-white outline-none focus:border-[#c8cb34]"
              placeholder="Tell us about your current outreach and goals"
            ></textarea>
          </label>

          <button
            class="w-full rounded-md px-5 py-3 font-semibold text-black"
            :style="submitStyle"
            type="submit"
          >
            Submit Request
          </button>
        </form>
      </div>
    </div>
  </Teleport>
</template>

<script setup lang="ts">
import { computed, reactive, watch } from 'vue'

type LeadForm = {
  fullName: string
  email: string
  company: string
  leadGoal: string
  message: string
}

const props = defineProps<{ open: boolean }>()

const emit = defineEmits<{
  (e: 'close'): void
  (e: 'submit', payload: LeadForm): void
}>()

const form = reactive<LeadForm>({
  fullName: '',
  email: '',
  company: '',
  leadGoal: '',
  message: ''
})

const submitStyle = computed(() => ({
  background: 'linear-gradient(180deg, #c8cb34, #a0a22a)'
}))

watch(
  () => props.open,
  (isOpen) => {
    if (isOpen) {
      document.body.style.overflow = 'hidden'
      return
    }
    document.body.style.overflow = ''
  }
)

function closeModal() {
  emit('close')
}

function handleSubmit() {
  emit('submit', { ...form })
  closeModal()
}
</script>
