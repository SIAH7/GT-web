<script setup>
import { onMounted, onBeforeUnmount, ref } from 'vue'
import Lenis from 'lenis'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import Preloader from './components/Preloader.vue'
import CustomCursor from './components/CustomCursor.vue'
import NavBar from './components/NavBar.vue'
import HeroSection from './components/HeroSection.vue'
import MarqueeStrip from './components/MarqueeStrip.vue'
import AboutSection from './components/AboutSection.vue'
import ServicesSection from './components/ServicesSection.vue'
import StatsSection from './components/StatsSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import GreenSection from './components/GreenSection.vue'
import ProcessSection from './components/ProcessSection.vue'
import ContactSection from './components/ContactSection.vue'
import FooterSection from './components/FooterSection.vue'

gsap.registerPlugin(ScrollTrigger)

const ready = ref(false)
const progress = ref(0)
let lenis, tick

onMounted(() => {
  document.body.classList.add('locked')
  lenis = new Lenis({ lerp: 0.09 })
  lenis.on('scroll', (e) => {
    ScrollTrigger.update()
    progress.value = e.limit ? e.scroll / e.limit : 0
  })
  tick = (t) => lenis.raf(t * 1000)
  gsap.ticker.add(tick)
  gsap.ticker.lagSmoothing(0)
  window.__lenis = lenis
})

function onDone() {
  document.body.classList.remove('locked')
  ready.value = true
  requestAnimationFrame(() => ScrollTrigger.refresh())
}

onBeforeUnmount(() => {
  gsap.ticker.remove(tick)
  lenis?.destroy()
})
</script>

<template>
  <Preloader @done="onDone" />
  <CustomCursor />
  <div class="progress" :style="{ transform: `scaleX(${progress})` }"></div>
  <NavBar :ready="ready" />
  <main>
    <HeroSection :ready="ready" />
    <MarqueeStrip />
    <AboutSection />
    <ServicesSection />
    <StatsSection />
    <ProjectsSection />
    <GreenSection />
    <ProcessSection />
    <ContactSection />
  </main>
  <FooterSection />
</template>

<style>
.progress {
  position: fixed; top: 0; left: 0; right: 0; height: 3px; z-index: 300;
  background: linear-gradient(90deg, var(--gold), var(--gold-2));
  transform-origin: left; transform: scaleX(0);
}
</style>
