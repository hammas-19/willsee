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

        <form class="space-y-4" @submit.prevent="submitForm">
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
              <span class="mb-1 block text-white/80">Contact Number</span>
              <input
                v-model="form.contactNumber"
                class="w-full rounded-md border border-white/20 bg-black/40 px-3 py-2 text-white outline-none focus:border-[#c8cb34]"
                type="tel"
                placeholder="+1 (555) 123-4567"
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
            {{ result || 'Submit Request' }}
          </button>

          <p
            v-if="status"
            class="text-sm"
            :class="status === 'success' ? 'text-[#c8cb34]' : 'text-red-400'"
          >
            {{ status === 'success' ? 'Thanks, we will be in touch shortly.' : result }}
          </p>
        </form>
      </div>
    </div>
  </Teleport>
</template>

<script setup lang="ts">
import { computed, reactive, ref, watch } from 'vue'

type LeadForm = {
  access_key: string
  subject: string
  fullName: string
  email: string
  company: string
  contactNumber: string
  message: string
}

const props = defineProps<{ open: boolean }>()

const emit = defineEmits<{
  (e: 'close'): void
}>()

const form = reactive<LeadForm>({
  access_key: 'YOUR_ACCESS_KEY_HERE',
  subject: 'New Submission from Web3Forms',
  fullName: '',
  email: '',
  company: '',
  contactNumber: '',
  message: ''
})

const result = ref('')
const status = ref('')

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

const submitForm = async () => {
  result.value = 'Please wait...'

  try {
    const response = await $fetch('https://api.web3forms.com/submit', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: form
    })

    result.value = response.message

    if (response.status === 200) {
      status.value = 'success'
      closeModal()
    } else {
      status.value = 'error'
    }
  } catch (error) {
    console.log(error)
    status.value = 'error'
    result.value = 'Something went wrong!'
  } finally {
    form.fullName = ''
    form.email = ''
    form.company = ''
    form.contactNumber = ''
    form.message = ''

    setTimeout(() => {
      result.value = ''
      status.value = ''
    }, 5000)
  }
}
</script>
