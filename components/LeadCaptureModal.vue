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
            <p class="text-xs uppercase tracking-[0.18em] text-[#c8cb34]">Convertixz</p>
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

  <Teleport to="body">
    <div v-if="showThankYou" class="fixed inset-0 z-50 flex items-center justify-center px-4">
      <button
        aria-label="Dismiss thank you overlay"
        class="absolute inset-0 bg-black/70 backdrop-blur-sm"
        type="button"
        @click="dismissThankYou"
      ></button>

      <div class="relative z-10 w-full max-w-lg rounded-2xl border border-[#c8cb34]/30 bg-[#111111] p-6 text-white shadow-2xl md:p-8">
        <p class="text-xs uppercase tracking-[0.18em] text-[#c8cb34]">Convertixz</p>
        <h3 class="mt-2 text-2xl font-serif md:text-3xl">Thank you</h3>
        <p class="mt-3 text-sm leading-relaxed text-white/75">
          Your request was submitted successfully. We’ll review it and reach out shortly.
        </p>
      </div>
    </div>
  </Teleport>
</template>

<script setup lang="ts">
import { computed, onBeforeUnmount, reactive, ref, watch } from 'vue'

type LeadForm = {
  access_key: string
  subject: string
  fullName: string
  email: string
  company: string
  contactNumber: string
  message: string
}

type Web3FormsResponse = {
  message?: string
}

const props = defineProps<{ open: boolean }>()

const emit = defineEmits<{
  (e: 'close'): void
}>()

const form = reactive<LeadForm>({
  access_key: '853044cb-b4a5-4979-b92c-665cd6efd636',
  subject: 'New Submission from Web3Forms',
  fullName: '',
  email: '',
  company: '',
  contactNumber: '',
  message: ''
})

const result = ref('')
const status = ref('')
const showThankYou = ref(false)
let thankYouTimeout: ReturnType<typeof setTimeout> | undefined

const submitStyle = computed(() => ({
  background: 'linear-gradient(180deg, #c8cb34, #a0a22a)'
}))

const isModalVisible = computed(() => props.open || showThankYou.value)

watch(
  isModalVisible,
  (isVisible) => {
    if (typeof document !== 'undefined') {
      document.body.style.overflow = isVisible ? 'hidden' : ''
    }
  },
  { immediate: true }
)

watch(
  () => props.open,
  (isOpen) => {
    if (isOpen) {
      showThankYou.value = false
    }
  }
)

function closeModal() {
  emit('close')
}

function dismissThankYou() {
  if (thankYouTimeout) {
    clearTimeout(thankYouTimeout)
    thankYouTimeout = undefined
  }

  showThankYou.value = false
}

function resetForm() {
  form.fullName = ''
  form.email = ''
  form.company = ''
  form.contactNumber = ''
  form.message = ''
}

function openThankYou() {
  if (thankYouTimeout) {
    clearTimeout(thankYouTimeout)
  }

  showThankYou.value = true
  thankYouTimeout = setTimeout(() => {
    showThankYou.value = false
    thankYouTimeout = undefined
  }, 4000)
}

const submitForm = async () => {
  result.value = 'Please wait...'
  status.value = ''

  try {
    const response = await fetch('https://api.web3forms.com/submit', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(form)
    })

    const data = (await response.json()) as Web3FormsResponse
    result.value = data.message ?? 'Request submitted.'

    if (response.ok) {
      status.value = 'success'
      resetForm()
      closeModal()
      openThankYou()
    } else {
      status.value = 'error'
      resetForm()
    }
  } catch (error) {
    console.log(error)
    status.value = 'error'
    result.value = 'Something went wrong!'
    resetForm()
  }

  setTimeout(() => {
    result.value = ''
    status.value = ''
  }, 5000)
}

onBeforeUnmount(() => {
  if (thankYouTimeout) {
    clearTimeout(thankYouTimeout)
  }

  if (typeof document !== 'undefined') {
    document.body.style.overflow = ''
  }
})
</script>
