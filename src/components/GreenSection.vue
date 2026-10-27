<script setup>
import { onMounted, ref } from 'vue'
import gsap from 'gsap'

const root = ref(null)
const items = ['Gestión ambiental', 'Factibilidad y diseño', 'Consultoría ambiental']

onMounted(() => {
  gsap.context(() => {
    // Sin pin: la animación avanza mientras la sección entra al viewport
    const tl = gsap.timeline({ scrollTrigger: { trigger: root.value, start: 'top 85%', end: 'center 45%', scrub: 0.6 } })
    tl.to('.gr-bg', { backgroundColor: '#0a2a1f', duration: 1, ease: 'none' }, 0)
      .fromTo('.leaf-ring', { scale: 0.5, opacity: 0 }, { scale: 1, opacity: 1, stagger: 0.1, duration: 1 }, 0)
      .from('.gr-text > *', { y: 40, opacity: 0, stagger: 0.12, duration: 0.8 }, 0.15)
      .from('.chip', { scale: 0.6, opacity: 0, stagger: 0.1, duration: 0.5 }, 0.6)
  }, root.value)
})
</script>

<template>
  <section ref="root" id="green" class="green">
    <div class="gr-bg"></div>
    <div class="rings"><i class="leaf-ring"></i><i class="leaf-ring"></i><i class="leaf-ring"></i></div>
    <div class="gr-text">
      <p class="eyebrow" style="color: var(--green)">GreenTowers Solutions</p>
      <h2 class="title">Construir hoy <em style="color: var(--green)">cuidando el mañana</em></h2>
      <p class="p">Nuestra área ambiental acompaña tus proyectos con gestión ambiental, factibilidad y diseño para minimizar el impacto sobre el entorno.</p>
      <div class="chips"><span class="chip" v-for="i in items" :key="i">{{ i }}</span></div>
    </div>
  </section>
</template>

<style scoped>
.green { min-height: 90vh; display: grid; place-items: center; overflow: hidden; padding-block: 0; }
.gr-bg { position: absolute; inset: 0; background: var(--bg); }
.rings { position: absolute; inset: 0; display: grid; place-items: center; pointer-events: none; }
.leaf-ring { grid-area: 1/1; border-radius: 50%; border: 1px solid rgba(63, 191, 132, .35); }
.leaf-ring:nth-child(1) { width: 40vmin; height: 40vmin; }
.leaf-ring:nth-child(2) { width: 70vmin; height: 70vmin; border-style: dashed; animation: spin 60s linear infinite; }
.leaf-ring:nth-child(3) { width: 100vmin; height: 100vmin; border-color: rgba(63, 191, 132, .15); }
@keyframes spin { to { rotate: 360deg; } }
.gr-text { position: relative; text-align: center; max-width: 48rem; }
.p { margin: 1.5rem auto 2rem; color: #a7c9ba; max-width: 36rem; }
.chips { display: flex; gap: .8rem; justify-content: center; flex-wrap: wrap; }
.chip { padding: .6rem 1.2rem; border-radius: 999px; border: 1px solid var(--green); color: var(--green); font-size: .85rem; }
.eyebrow::before { background: var(--green); }
</style>
