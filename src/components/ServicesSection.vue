<script setup>
import { onMounted, ref } from 'vue'
import gsap from 'gsap'

const root = ref(null)
const services = [
  { n: '01', t: 'Arquitectura y diseño', d: 'Concebimos espacios funcionales y estéticos, desde el primer boceto hasta los planos constructivos.', icon: 'M3 21h18M5 21V8l7-5 7 5v13M9 21v-6h6v6' },
  { n: '02', t: 'Construcción', d: 'Ejecutamos obras residenciales, corporativas y comerciales con control de tiempos y costos.', icon: 'M2 20h20M4 20V10l8-6 8 6v10M8 20v-5h8v5' },
  { n: '03', t: 'Supervisión', d: 'Supervisamos de cerca cada proyecto con aseguramiento de calidad en cada etapa.', icon: 'M2 12s4-7 10-7 10 7 10 7-4 7-10 7S2 12 2 12zM12 9a3 3 0 100 6 3 3 0 000-6z' },
  { n: '04', t: 'Consultoría', d: 'Asesoría técnica y de factibilidad para que tomes decisiones seguras sobre tu inversión.', icon: 'M4 4h16v12H8l-4 4zM8 9h8M8 12h5' },
]

function tilt(e) {
  const c = e.currentTarget, r = c.getBoundingClientRect()
  const x = (e.clientX - r.left) / r.width - 0.5, y = (e.clientY - r.top) / r.height - 0.5
  gsap.to(c, { rotateY: x * 14, rotateX: -y * 14, duration: 0.5, transformPerspective: 900, ease: 'power2.out' })
  c.style.setProperty('--mx', `${(x + 0.5) * 100}%`); c.style.setProperty('--my', `${(y + 0.5) * 100}%`)
}
const reset = (e) => gsap.to(e.currentTarget, { rotateX: 0, rotateY: 0, duration: 0.8, ease: 'elastic.out(1,.5)' })

onMounted(() => {
  gsap.context(() => {
    gsap.from('.sv-title .line-mask > span', { yPercent: 110, stagger: 0.12, duration: 1, ease: 'expo.out', scrollTrigger: { trigger: '.sv-title', start: 'top 80%' } })
    gsap.from('.card', { y: 90, opacity: 0, stagger: 0.14, duration: 1, ease: 'power3.out', scrollTrigger: { trigger: '.cards', start: 'top 80%' } })
  }, root.value)
})
</script>

<template>
  <section ref="root" id="servicios" class="services">
    <p class="eyebrow">Servicios</p>
    <h2 class="title sv-title">
      <span class="line-mask"><span>Todo lo que tu obra</span></span>
      <span class="line-mask"><span><em>necesita</em>, en un solo equipo</span></span>
    </h2>
    <div class="cards">
      <article v-for="s in services" :key="s.n" class="card" data-cursor="Ver" @mousemove="tilt" @mouseleave="reset">
        <span class="num">{{ s.n }}</span>
        <svg width="44" height="44" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.4" stroke-linecap="round" stroke-linejoin="round"><path :d="s.icon" /></svg>
        <h3>{{ s.t }}</h3>
        <p>{{ s.d }}</p>
      </article>
    </div>
  </section>
</template>

<style scoped>
.cards { margin-top: 4rem; display: grid; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr)); gap: 1.3rem; }
.card {
  position: relative; padding: 2rem; border-radius: 1.2rem; border: 1px solid var(--line); background: var(--bg-2);
  overflow: hidden; transform-style: preserve-3d; min-height: 20rem; display: flex; flex-direction: column;
}
.card::before { content: ''; position: absolute; inset: 0; background: radial-gradient(circle 220px at var(--mx, 50%) var(--my, 50%), rgba(212, 166, 58, .22), transparent 70%); opacity: 0; transition: opacity .4s; }
.card:hover::before { opacity: 1; }
.card > * { position: relative; }
.num { font-family: var(--font-display); color: var(--muted); font-size: .8rem; letter-spacing: .2em; margin-bottom: auto; }
.card svg { color: var(--gold); margin: 2.5rem 0 1.2rem; }
.card h3 { font-family: var(--font-display); font-size: 1.35rem; margin-bottom: .7rem; }
.card p { color: var(--muted); font-size: .92rem; }
</style>
