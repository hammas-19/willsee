<template>
  <div class="bg-[#0b0b0b] text-white">
    <HeroSection @open-form="isModalOpen = true" />

    <section class="max-w-7xl mx-auto px-6 py-16 md:py-20">
      <h2 class="text-3xl md:text-5xl font-serif text-center mb-5">Growth Built Around Results</h2>
      <p class="text-center text-white/80 max-w-3xl mx-auto leading-relaxed">
        Convertix is a modern lead generation partner focused on helping companies attract, engage, and convert the right customers.
        We combine data-driven outreach, conversion-focused systems, and scalable growth strategies to help businesses create consistent opportunities without wasting time on low-quality leads.
        From startups to growing brands, we build acquisition systems that turn attention into revenue.
      </p>
    </section>

    <section class="max-w-7xl mx-auto px-6 pb-16 md:pb-20">
      <h2 class="text-3xl md:text-5xl font-serif text-center mb-10">What We Do</h2>
      <div class="grid gap-5 sm:grid-cols-2 lg:grid-cols-3">
        <article v-for="service in services" :key="service.title" class="rounded-2xl border border-white/10 bg-white/5 p-6">
          <h3 class="text-xl font-semibold mb-2 text-[#d3d55d]">{{ service.title }}</h3>
          <p class="text-white/80 leading-relaxed">{{ service.description }}</p>
        </article>
      </div>
    </section>

    <section class="max-w-7xl mx-auto px-6 pb-16 md:pb-20">
      <h2 class="text-3xl md:text-5xl font-serif text-center mb-10">Why Brands Choose Convertix</h2>
      <div class="grid gap-4 md:grid-cols-2 lg:grid-cols-3">
        <div v-for="point in whyConvertix" :key="point.title" class="rounded-xl border border-white/10 bg-black/40 p-5">
          <h3 class="font-semibold mb-2">{{ point.title }}</h3>
          <p class="text-white/75">{{ point.description }}</p>
        </div>
      </div>
    </section>

    <section class="py-16 md:py-20">
      <h2 class="text-3xl md:text-5xl font-serif text-center mb-12">What Clients Say</h2>
      
      <!-- First Marquee Row (Left to Right) -->
      <div class="mb-6 relative overflow-hidden group">
        <div class="fade-left absolute inset-y-0 left-0 w-16 md:w-32 z-10 pointer-events-none"></div>
        <div class="fade-right absolute inset-y-0 right-0 w-16 md:w-32 z-10 pointer-events-none"></div>
        
        <div class="marquee-track marquee-ltr" :style="{ animationPlayState: isTestimonialsPaused ? 'paused' : 'running' }" @mouseenter="isTestimonialsPaused = true" @mouseleave="isTestimonialsPaused = false">
          <div class="marquee-row" v-for="batch in 3" :key="`ltr-batch-${batch}`">
            <div v-for="(testimonial, i) in testimonials.slice(0, 2)" :key="`row1-${batch}-${i}`" class="testimonial-card">
              <p class="mb-4 text-white/85 leading-relaxed text-sm">{{ testimonial.quote }}</p>
              <div class="flex items-center gap-3">
                <div class="w-10 h-10 rounded-full bg-gradient-to-br from-[#c8cb34] to-[#a0a22a] flex items-center justify-center text-black font-bold text-xs flex-shrink-0">{{ testimonial.initials }}</div>
                <div class="min-w-0">
                  <p class="font-semibold text-sm">{{ testimonial.name }}</p>
                  <p class="text-xs text-white/60 truncate">{{ testimonial.company }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Second Marquee Row (Right to Left) -->
      <div class="relative overflow-hidden group">
        <div class="fade-left absolute inset-y-0 left-0 w-16 md:w-32 z-10 pointer-events-none"></div>
        <div class="fade-right absolute inset-y-0 right-0 w-16 md:w-32 z-10 pointer-events-none"></div>
        
        <div class="marquee-track marquee-rtl" :style="{ animationPlayState: isTestimonialsPaused ? 'paused' : 'running' }" @mouseenter="isTestimonialsPaused = true" @mouseleave="isTestimonialsPaused = false">
          <div class="marquee-row" v-for="batch in 3" :key="`rtl-batch-${batch}`">
            <div v-for="(testimonial, i) in testimonials.slice(2)" :key="`row2-${batch}-${i}`" class="testimonial-card">
              <p class="mb-4 text-white/85 leading-relaxed text-sm">{{ testimonial.quote }}</p>
              <div class="flex items-center gap-3">
                <div class="w-10 h-10 rounded-full bg-gradient-to-br from-[#c8cb34] to-[#a0a22a] flex items-center justify-center text-black font-bold text-xs flex-shrink-0">{{ testimonial.initials }}</div>
                <div class="min-w-0">
                  <p class="font-semibold text-sm">{{ testimonial.name }}</p>
                  <p class="text-xs text-white/60 truncate">{{ testimonial.company }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section class="max-w-5xl mx-auto px-6 pb-20 text-center">
      <div class="rounded-3xl border border-[#c8cb34]/30 bg-[#c8cb34]/10 p-8 md:p-10">
        <h2 class="text-3xl md:text-5xl font-serif mb-4">Ready to Scale Your Pipeline?</h2>
        <p class="text-white/85 max-w-3xl mx-auto mb-8">
          Stop chasing cold prospects and start building a predictable lead generation system that drives measurable growth.
        </p>
        <div class="flex flex-wrap items-center justify-center gap-3">
          <button
            type="button"
            class="px-6 py-3 rounded-md bg-[#c8cb34] text-black font-semibold"
            @click="isModalOpen = true"
          >
            Schedule a Free Consultation
          </button>
          <button
            type="button"
            class="px-6 py-3 rounded-md border border-white/25 bg-white/5 text-white font-semibold"
            @click="isModalOpen = true"
          >
            Let's Talk Growth
          </button>
        </div>
      </div>
    </section>

    <footer class="border-t border-white/10 py-8 text-center text-sm text-white/60">
      <p>Convertix</p>
      <p>Turning Prospects Into Results.</p>
      <p class="mt-3 text-white/80">Contact</p>
      <p class="mt-1">hello@convertix.com</p>
      <p>www.convertix.com</p>
      <p class="mt-3 text-white/80">Follow</p>
      <p class="mt-1">LinkedIn · Instagram · Twitter/X</p>
      <p class="mt-4">© 2026 Convertix. All rights reserved.</p>
    </footer>

    <LeadCaptureModal
      :open="isModalOpen"
      @close="isModalOpen = false"
      @submit="handleLeadSubmit"
    />
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'
import HeroSection from '~/components/HeroSection.vue'
import LeadCaptureModal from '~/components/LeadCaptureModal.vue'

type LeadPayload = {
  fullName: string
  email: string
  company: string
  leadGoal: string
  message: string
}

const isModalOpen = ref(false)
const isTestimonialsPaused = ref(false)

const services = [
  {
    title: 'Targeted Lead Generation',
    description: 'We identify and connect you with decision-makers actively interested in your offer through precise targeting and outreach systems.'
  },
  {
    title: 'Cold Email Outreach',
    description: 'Personalized outbound campaigns designed to start meaningful conversations and generate qualified appointments at scale.'
  },
  {
    title: 'Sales Funnel Optimization',
    description: 'Landing pages, messaging, and conversion flows optimized to increase response rates and maximize ROI.'
  },
  {
    title: 'Appointment Setting',
    description: 'We help fill your calendar with qualified prospects so your sales team can focus on closing deals.'
  },
  {
    title: 'B2B Prospecting',
    description: 'Advanced prospect research and segmentation tailored to your industry, market, and ideal customer profile.'
  },
  {
    title: 'Growth Automation',
    description: 'Smart automation systems that streamline outreach, follow-ups, and lead management for faster scaling.'
  }
]

const whyConvertix = [
  {
    title: 'Precision Targeting',
    description: 'We focus on high-intent prospects that align with your business goals.'
  },
  {
    title: 'Scalable Systems',
    description: 'Our growth frameworks are designed to scale consistently as your business grows.'
  },
  {
    title: 'Data-Driven Decisions',
    description: 'Every campaign is optimized using performance insights and measurable analytics.'
  },
  {
    title: 'Quality Over Volume',
    description: 'We prioritize meaningful opportunities instead of inflated lead numbers.'
  },
  {
    title: 'Conversion-Focused Strategy',
    description: 'Everything we build is designed around generating revenue, not just traffic.'
  },
  {
    title: 'Modern Growth Approach',
    description: 'We combine automation, strategy, and creative outreach to stay ahead in competitive markets.'
  }
]

const testimonials = [
  {
    quote: 'Convertix completely transformed our outreach process and helped us generate consistent inbound opportunities.',
    name: 'Morgan Baume',
    company: 'Alchemy Plumbing',
    initials: 'MB'
  },
  {
    quote: 'The quality of leads and professionalism of the campaigns exceeded our expectations.',
    name: 'Jeff Seale',
    company: 'Accurate Electric Plumbing, Heating & Air',
    initials: 'JS'
  },
  {
    quote: 'Their systems gave our sales team a predictable pipeline we could finally scale.',
    name: 'Corson Searles',
    company: 'Identity Shift Hockey',
    initials: 'CS'
  }
]

function handleLeadSubmit(payload: LeadPayload) {
  // Placeholder for backend integration (API, CRM, email webhook)
  console.log('Lead submitted:', payload)
}
</script>

<style scoped>
.testimonial-card {
  flex-shrink: 0;
  width: 360px;
  border: 1px solid rgba(200, 203, 52, 0.4);
  border-radius: 0.75rem;
  background: rgba(20, 20, 20, 0.6);
  padding: 1.5rem;
  margin-right: 1rem;
}

.marquee-track {
  display: flex;
  will-change: transform;
  padding: 1px 0;
}

.marquee-track.marquee-ltr {
  animation: marquee-ltr 50s linear infinite;
}

.marquee-track.marquee-rtl {
  animation: marquee-rtl 50s linear infinite;
}

.marquee-row {
  display: flex;
  flex-shrink: 0;
  width: max-content;
}

.fade-left {
  background: linear-gradient(90deg, rgba(11, 11, 11, 0.98), transparent);
}

.fade-right {
  background: linear-gradient(270deg, rgba(11, 11, 11, 0.98), transparent);
}

@keyframes marquee-ltr {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(calc(-33.333%));
  }
}

@keyframes marquee-rtl {
  0% {
    transform: translateX(calc(-33.333%));
  }
  100% {
    transform: translateX(0);
  }
}
</style>
