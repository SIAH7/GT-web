<script setup>
import { onMounted, ref, watch } from 'vue'
import gsap from 'gsap'

const props = defineProps({ ready: Boolean })
const root = ref(null)
const go = (h) => window.__lenis?.scrollTo(h)
const buildings = Array.from({ length: 22 }, (_, i) => ({
  x: i * 5.2,
  w: 3 + ((i * 7) % 4),
  h: 18 + ((i * 37) % 52),
}))

onMounted(() => {
  gsap.context(() => {
    gsap.to('.layer-back', { yPercent: 12, ease: 'none', scrollTrigger: { trigger: root.value, start: 'top top', end: 'bottom top', scrub: true } })
    gsap.to('.layer-front', { yPercent: 28, ease: 'none', scrollTrigger: { trigger: root.value, start: 'top top', end: 'bottom top', scrub: true } })
    gsap.to('.hero-content', { yPercent: -8, ease: 'none', scrollTrigger: { trigger: root.value, start: 'top top', end: 'bottom top', scrub: true } })
    root.value.addEventListener('mousemove', (e) => {
      const x = (e.clientX / innerWidth - 0.5), y = (e.clientY / innerHeight - 0.5)
      gsap.to('.layer-back', { x: x * -20, duration: 1.2 })
      gsap.to('.layer-front', { x: x * -50, duration: 1.2 })
      gsap.to('.sun', { x: x * 30, y: y * 20, duration: 1.5 })
    })
  }, root.value)
})

watch(() => props.ready, (r) => {
  if (!r) return
  const tl = gsap.timeline({ delay: 0.1 })
  tl.from('.hero h1 .line-mask > span', { yPercent: 110, rotate: 3, stagger: 0.12, duration: 1.1, ease: 'expo.out' })
    .from('.hero-sub, .hero-actions', { y: 30, opacity: 0, stagger: 0.15, duration: 0.9 }, '-=0.6')
    .from('.skyline rect.b', { scaleY: 0, transformOrigin: 'bottom', stagger: 0.04, duration: 1.2, ease: 'power3.out' }, 0)
    .from('.scroll-hint', { opacity: 0, y: 20 }, '-=0.4')
})
</script>

<template>
  <section ref="root" class="hero" id="inicio">
    <div class="sun"></div>
    <svg class="skyline layer-back" viewBox="0 0 115 80" preserveAspectRatio="xMidYMax slice">
      <rect v-for="(b, i) in buildings" :key="i" class="b" :x="b.x" :y="80 - b.h - 10" :width="b.w + 2" :height="b.h + 10" fill="#101a31" />
    </svg>
    <svg class="skyline layer-front" viewBox="0 0 100 80" preserveAspectRatio="xMidYMax slice">
      <defs>
        <pattern id="win" width="2" height="2.4" patternUnits="userSpaceOnUse"><rect x=".5" y=".6" width=".8" height="1" fill="#d4a63a" opacity=".55" /></pattern>
        <linearGradient id="bg" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#18233f" /><stop offset="1" stop-color="#0b1220" /></linearGradient>
      </defs>
      <g v-for="(b, i) in [[6,12,34],[19,10,50],[31,14,64],[48,12,44],[62,16,58],[80,11,38],[91,9,28]]" :key="i">
        <rect class="b" :x="b[0]" :y="80 - b[2]" :width="b[1]" :height="b[2]" fill="url(#bg)" />
        <rect class="b" :x="b[0]" :y="80 - b[2]" :width="b[1]" :height="b[2]" fill="url(#win)" />
      </g>
      <rect x="0" y="79" width="100" height="1" fill="#d4a63a" opacity=".5" />
    </svg>

    <div class="hero-content">
      <p class="eyebrow">Golden Towers S.A. de C.V. · El Salvador</p>
      <h1 class="title big">
        <span class="line-mask"><span>Cuando la pasión</span></span>
        <span class="line-mask"><span>se encuentra con la</span></span>
        <span class="line-mask"><span><em>determinación</em></span></span>
      </h1>
      <p class="hero-sub">Arquitectura, diseño, construcción, supervisión y consultoría. Espacios cómodos y funcionales que transforman tu entorno.</p>
      <div class="hero-actions">
        <a href="#proyectos" class="btn" data-cursor="Ver" @click.prevent="go('#proyectos')">Ver proyectos</a>
        <a href="#contacto" class="btn ghost" @click.prevent="go('#contacto')">Trabajemos juntos</a>
      </div>
    </div>
    <div class="scroll-hint"><span></span>Scroll</div>
  </section>
</template>

<style scoped>
.hero { min-height: 100vh; min-height: 100svh; display: flex; align-items: center; overflow: hidden; background: radial-gradient(120% 80% at 70% 0%, #1b2a4d 0%, var(--bg) 60%); }
.sun { position: absolute; width: 38vmax; height: 38vmax; right: -6vmax; top: 4vmax; border-radius: 50%; background: radial-gradient(circle, rgba(243, 210, 122, .35), rgba(212, 166, 58, .08) 50%, transparent 70%); filter: blur(10px); }
.skyline { position: absolute; left: 0; bottom: 0; width: 100%; height: 75%; }
.layer-back { opacity: .8; }
.hero-content { position: relative; z-index: 2; max-width: 62rem; padding-top: 6rem; padding-bottom: 5rem; }
.hero-content::before { content: ''; position: absolute; inset: 0 -10vw 0 -10vw; z-index: -1; background: linear-gradient(90deg, rgba(8, 13, 24, .85), rgba(8, 13, 24, .55) 60%, transparent); }
.big { font-size: clamp(2rem, 4.6vw, 4.2rem); line-height: 1.08; }
.hero-sub { margin-top: 1.5rem; max-width: 34rem; color: var(--muted); font-size: clamp(1rem, 1.3vw, 1.15rem); }
.hero-actions { margin-top: 2rem; display: flex; gap: 1rem; flex-wrap: wrap; }
.scroll-hint { position: absolute; bottom: 1.8rem; left: 50%; translate: -50%; display: flex; flex-direction: column; align-items: center; gap: .6rem; font-size: .65rem; letter-spacing: .3em; text-transform: uppercase; color: var(--muted); z-index: 3; }
.scroll-hint span { width: 1px; height: 44px; background: linear-gradient(var(--gold), transparent); animation: drip 1.8s infinite; transform-origin: top; }
@keyframes drip { 0% { transform: scaleY(0); } 50% { transform: scaleY(1); } 100% { transform: scaleY(1); opacity: 0; } }
</style>
