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
      <div class="grid gap-6 sm:grid-cols-2 lg:grid-cols-3">
        <div
          v-for="service in services"
          :key="service.title"
          class="service-card group relative overflow-hidden rounded-2xl border border-white/10 bg-gradient-to-br from-white/5 to-white/0 p-8 transition-all duration-300"
          @mousemove="handleMouseMove"
          @mouseleave="handleMouseLeave"
        >
          <!-- Pointer follower -->
          <div class="pointer-follower absolute inset-0 pointer-events-none opacity-0 group-hover:opacity-100" :style="follerStyle"></div>

          <div class="relative z-10">
            <div class="mb-4 flex items-center justify-start">
              <div v-html="service.icon" :class="[service.iconSize || 'w-12 h-12', 'text-[#d3d55d]']"></div>
            </div>
            <h3 class="text-2xl font-semibold mb-3 text-[#d3d55d] transition-colors duration-300 group-hover:text-[#e8ec5d]">{{ service.title }}</h3>
            <p class="text-white/80 leading-relaxed text-base transition-colors duration-300 group-hover:text-white/90">{{ service.description }}</p>
          </div>
        </div>
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

    <div class="testimonials-section-wrapper">
      <section class="py-16 md:py-20">
        <h2 class="text-3xl md:text-5xl font-serif text-center mb-12">What Clients Say</h2>
        
        <!-- Single Infinite Marquee Row -->
        <div class="relative overflow-hidden group">
          <div class="fade-left absolute inset-y-0 left-0 w-16 md:w-32 z-10 pointer-events-none"></div>
          <div class="fade-right absolute inset-y-0 right-0 w-16 md:w-32 z-10 pointer-events-none"></div>
          
          <div class="marquee-track marquee-ltr">
            <div class="marquee-row" v-for="batch in 6" :key="`infinite-batch-${batch}`">
              <div v-for="(testimonial, i) in testimonials" :key="`infinite-${batch}-${i}`" class="testimonial-card">
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
    </div>

    <footer class="border-t border-white/10 bg-black py-12 text-white">
      <div class="max-w-7xl mx-auto px-6">
        <div class="grid grid-cols-1 md:grid-cols-3 gap-8 mb-8">
          <!-- Brand -->
          <div>
            <img src="/typoLogo.jpg" alt="Convertix" class="h-16 md:h-20 w-auto mb-2 object-contain" />
            <p class="text-white/60">Turning Prospects Into Results.</p>
          </div>

          <!-- Contact -->
          <div>
            <h4 class="font-semibold mb-3 text-white/80">Contact</h4>
            <p class="text-[#c8cb34] mb-2 hover:text-[#e8ec5d] transition-colors">
              <a href="mailto:hello@convertix.com" class="text-inherit">hello@convertix.com</a>
            </p>
            <p class="text-[#c8cb34] hover:text-[#e8ec5d] transition-colors">
              <a href="https://www.convertix.com" target="_blank" class="text-inherit">www.convertix.com</a>
            </p>
          </div>

          <!-- Social -->
          <div>
            <h4 class="font-semibold mb-3 text-white/80">Follow Us</h4>
            <div class="flex gap-4">
              <a href="https://linkedin.com" target="_blank" class="w-8 h-8 rounded-full border border-[#c8cb34]/50 text-[#c8cb34] flex items-center justify-center hover:border-[#e8ec5d] hover:text-[#e8ec5d] transition-colors" title="LinkedIn">
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                  <path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6zM2 9h4v12H2z"></path>
                  <circle cx="4" cy="4" r="2"></circle>
                </svg>
              </a>
              <a href="https://instagram.com" target="_blank" class="w-8 h-8 rounded-full border border-[#c8cb34]/50 text-[#c8cb34] flex items-center justify-center hover:border-[#e8ec5d] hover:text-[#e8ec5d] transition-colors" title="Instagram">
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                  <rect x="2" y="2" width="20" height="20" rx="5" ry="5"></rect>
                  <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"></path>
                  <circle cx="17.5" cy="6.5" r="1.5"></circle>
                </svg>
              </a>
              <a href="https://twitter.com" target="_blank" class="w-8 h-8 rounded-full border border-[#c8cb34]/50 text-[#c8cb34] flex items-center justify-center hover:border-[#e8ec5d] hover:text-[#e8ec5d] transition-colors" title="Twitter/X">
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="currentColor">
                  <path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24h-6.6l-5.17-6.763-5.91 6.763h-3.308l7.73-8.835L2.55 2.25h6.556l4.702 6.217 5.436-6.217zM17.15 18.344h1.828L6.122 4.125H4.231l12.919 14.219z"></path>
                </svg>
              </a>
            </div>
          </div>
        </div>

        <!-- Divider -->
        <div class="border-t border-white/10 pt-8">
          <p class="text-center text-white/50 text-sm">© 2026 Convertix. All rights reserved.</p>
        </div>
      </div>
    </footer>

    <LeadCaptureModal
      :open="isModalOpen"
      @close="isModalOpen = false"
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
  contactNumber: string
  message: string
}

const isModalOpen = ref(false)
const follerStyle = ref({})

const services = [
  {
    title: 'Targeted Lead Generation',
    description: 'We identify and connect you with decision-makers actively interested in your offer through precise targeting and outreach systems.',
    icon: '<svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 16 16"><path fill="currentColor" d="M8 0q.552.001 1.09.074c.337.047.499.424.324.716L9.4.814a.52.52 0 0 1-.517.243A6.995 6.995 0 0 0 1.003 8c0 3.87 3.13 7 7 7a6.995 6.995 0 0 0 6.944-7.88a.52.52 0 0 1 .243-.517l.022-.014c.292-.175.67-.013.716.324q.075.532.075 1.09c0 4.42-3.58 8-8 8s-8-3.58-8-8s3.58-8 8-8z"/><path fill="currentColor" d="M8 4c.177 0 .253.211.128.336l-.592.592a.7.7 0 0 1-.312.173a3 3 0 0 0-2.22 2.9c0 1.66 1.34 3 3 3c1.39 0 2.56-.944 2.9-2.22a.7.7 0 0 1 .173-.312l.592-.592c.126-.126.337-.05.337.128c0 2.21-1.79 4-4 4s-4-1.79-4-4s1.79-4 4-4z"/><path fill="currentColor" d="M12.6.008a.5.5 0 0 1 .405.395l.435 2.17l2.17.435a.5.5 0 0 1 .159.919l-2.5 1.5a.5.5 0 0 1-.257.071h-1.79l-2.35 2.35a.5.5 0 0 1-.707-.707l2.35-2.35v-1.79l.005-.067a.5.5 0 0 1 .066-.19l1.5-2.5l.044-.062A.5.5 0 0 1 12.6.01z"/></svg>'
  },
  {
    title: 'Cold Email Outreach',
    description: 'Personalized outbound campaigns designed to start meaningful conversations and generate qualified appointments at scale.',
    icon: '<svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24"><path fill="currentColor" d="M4.308 6L12 11l7.692-5zm.308 13q-.667 0-1.141-.475T3 17.386V6.615q0-.666.475-1.14T4.615 5h14.77q.666 0 1.14.475T21 6.615v5.577q0 .213-.144.357t-.357.143t-.356-.143t-.143-.357V6.885l-7.552 4.944q-.094.069-.448.13q-.125 0-.234-.027q-.108-.028-.214-.103L4 6.884v10.5q0 .27.173.443t.443.173H9.75q.213 0 .356.144t.144.357t-.144.356T9.75 19zm10.873.854l5.334-5.335q.14-.14.344-.15t.364.15t.16.354t-.16.354l-5.477 5.477q-.242.242-.565.242t-.566-.242l-2.638-2.639q-.14-.14-.15-.344t.15-.363t.354-.16t.353.16z"/></svg>',
    iconSize: 'w-16 h-16'
  },
  {
    title: 'Sales Funnel Optimization',
    description: 'Landing pages, messaging, and conversion flows optimized to increase response rates and maximize ROI.',
    icon: '<svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 32 32"><path fill="currentColor" d="m14.001 22.997l4 3.999l-4 4l-1.414-1.415l1.586-1.586H10a.99.99 0 0 1-.854-.511l-4.014-6.992l1.737-.993l3.712 6.496h3.591l-1.585-1.585zM28 13c-.16 0-.315.023-.469.047l-4.653-8.53A1 1 0 0 0 22 3.995h-4.169l1.585-1.585L18 .996l-3.998 4L18 8.994l1.415-1.414l-1.585-1.585h3.576l4.369 8.009A2.98 2.98 0 0 0 25 16c0 .768.297 1.462.773 1.992L22 24.907L10.878 4.517a1 1 0 0 0-1.755 0l-3.85 7.057l1.732 1L10 7.084l11.123 20.39a1 1 0 0 0 1.755 0l4.649-8.522c.155.025.31.048.473.048a3 3 0 1 0 0-6M7 15.996c0-1.655-1.345-3-3-3s-3 1.345-3 3s1.346 3 3 3s3-1.346 3-3m-2 0a1 1 0 1 1-2-.002a1 1 0 0 1 2 .002"/></svg>'
  },
  {
    title: 'Appointment Setting',
    description: 'We help fill your calendar with qualified prospects so your sales team can focus on closing deals.',
    icon: '<svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 48 48"><path fill="currentColor" d="M10.75 4c.69 0 1.25.56 1.25 1.25v5.5c0 .69-.56 1.25-1.25 1.25h-5.5a1.25 1.25 0 1 1 0-2.5H9.5V5.25c0-.69.56-1.25 1.25-1.25m26.5 0c.69 0 1.25.56 1.25 1.25V9.5h4.25a1.25 1.25 0 1 1 0 2.5h-5.5c-.69 0-1.25-.56-1.25-1.25v-5.5c0-.69.56-1.25 1.25-1.25M16.5 12a2.5 2.5 0 0 0-2.5 2.5v19a2.5 2.5 0 0 0 2.5 2.5h15a2.5 2.5 0 0 0 2.5-2.5v-19a2.5 2.5 0 0 0-2.5-2.5zm0 2.5h15v19h-15zm3.75 4.5a1.25 1.25 0 1 0 0 2.5h7.5a1.25 1.25 0 1 0 0-2.5zm0 5a1.25 1.25 0 1 0 0 2.5h4.5a1.25 1.25 0 1 0 0-2.5zM12 42.75a1.25 1.25 0 1 1-2.5 0V38.5H5.25a1.25 1.25 0 1 1 0-2.5h5.5c.69 0 1.25.56 1.25 1.25zm26.5 0a1.25 1.25 0 1 1-2.5 0v-5.5c0-.69.56-1.25 1.25-1.25h5.5a1.25 1.25 0 1 1 0 2.5H38.5z"/></svg>',
    iconSize: 'w-16 h-16'
  },
  {
    title: 'B2B Prospecting',
    description: 'Advanced prospect research and segmentation tailored to your industry, market, and ideal customer profile.',
    icon: '<svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24"><g fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"><path d="M16 2v4M8 2v4m13 7v-1c0-3.771 0-5.657-1.172-6.828S16.771 4 13 4h-2C7.229 4 5.343 4 4.172 5.172S3 8.229 3 12v2c0 3.771 0 5.657 1.172 6.828S7.229 22 11 22M3 10h18"/><path d="M13 19.5s1.348.507 2 2.5c0 0 3.177-5 6-6"/></g></svg>'
  },
  {
    title: 'Growth Automation',
    description: 'Smart automation systems that streamline outreach, follow-ups, and lead management for faster scaling.',
    icon: '<svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24"><path fill="currentColor" d="M4 19V7l8-6l8 6v4h-2V8l-6-4.5L6 8v9h6v2Zm14.5 3l-1.4-3.1l-3.1-1.4l3.1-1.4l1.4-3.1l1.4 3.1l3.1 1.4l-3.1 1.4Z"/></svg>',
    iconSize: 'w-16 h-16'
  }
]

const whyConvertix = [
  {
    title: 'Precision Targeting',
    description: 'We focus on high-intent prospects that align with your business goals.'
  },
  {
    title: 'Quality Monitoring System',
    description: 'Our quality monitoring systems ensure consistent performance, accuracy, and continuous improvement across every process.'
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
  // TODO: Integrate with backend API/CRM
}

function handleMouseMove(e: any) {
  const card = e.currentTarget as any
  const rect = card.getBoundingClientRect()
  const x = e.clientX - rect.left
  const y = e.clientY - rect.top

  follerStyle.value = {
    background: `radial-gradient(circle at 50% 50%, rgba(200, 203, 52, 0.5), transparent 70%)`,
    transform: `translate(${x - 120}px, ${y - 120}px)`,
    width: '240px',
    height: '240px',
    borderRadius: '50%',
    pointerEvents: 'none',
    filter: 'blur(45px)',
    transition: 'transform 0.8s ease-out'
  } as any
}

function handleMouseLeave() {
  follerStyle.value = {}
}
</script>

<style scoped>
.service-card {
  min-height: 280px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.service-card:hover {
  transform: translateY(-4px) scale(1.02);
}

.pointer-follower {
  transition: opacity 0.3s ease-out;
}

.testimonials-section-wrapper {
  background: linear-gradient(rgba(0, 0, 0, 0.95), rgba(0, 0, 0, 0.882)), url('/secBg.jpg');
  background-size: cover;
  background-position: center;
  position: relative;
  width: 100%;
}

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

.marquee-track:hover {
  animation-play-state: paused;
}

.marquee-track {
  animation-play-state: running;
}

.marquee-track.marquee-ltr {
  animation: marquee-ltr 20s linear infinite;
  animation-fill-mode: none;
}

.marquee-track.marquee-rtl {
  animation: marquee-rtl 20s linear infinite;
  animation-fill-mode: none;
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
  0% { transform: translateX(0); }
  100% { transform: translateX(calc(-25%)); }
}

@keyframes marquee-rtl {
  0% { transform: translateX(calc(-25%)); }
  100% { transform: translateX(0); }
}
</style>
