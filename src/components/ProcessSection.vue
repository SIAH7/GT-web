<script setup>
import { onMounted, ref } from 'vue'
import gsap from 'gsap'

const root = ref(null)
const go = (h) => window.__lenis?.scrollTo(h, { offset: -20, duration: 1.6 })
const steps = [
  { t: 'Consulta', d: 'Escuchamos tu idea, terreno y presupuesto.', tag: 'Semana 1', icon: 'M4 5h16v11H8l-4 4zM8 9h8M8 12h5' },
  { t: 'Diseño', d: 'Desarrollamos planos, renders y especificaciones.', tag: 'Semanas 2–4', icon: 'M4 20l4-1L19 8l-3-3L5 16zM14 7l3 3' },
  { t: 'Construcción', d: 'Ejecutamos la obra con cronograma claro.', tag: 'Ejecución', icon: 'M3 20h18M6 20V10l6-6 6 6v10M10 20v-5h4v5' },
  { t: 'Supervisión', d: 'Control de calidad constante en cada etapa.', tag: 'Continuo', icon: 'M2 12s4-7 10-7 10 7 10 7-4 7-10 7S2 12 2 12zM12 9a3 3 0 100 6 3 3 0 000-6z' },
  { t: 'Entrega', d: 'Te entregamos tu espacio listo para habitar.', tag: 'Llave en mano', icon: 'M8 15a4 4 0 110-8 4 4 0 010 8zM11 11h10v3M17 11v3' },
]

onMounted(() => {
  gsap.context(() => {
    gsap.fromTo('.rail-fill', { scaleY: 0 }, { scaleY: 1, ease: 'none', scrollTrigger: { trigger: '.steps', start: 'top 65%', end: 'bottom 65%', scrub: true } })
    gsap.from('.pr-intro > *', { y: 40, opacity: 0, stagger: 0.12, duration: 0.9, ease: 'power3.out', scrollTrigger: { trigger: '.pr-intro', start: 'top 80%' } })
    gsap.utils.toArray('.step').forEach((s) => {
      gsap.from(s.querySelector('.card'), { y: 50, opacity: 0, duration: 0.8, ease: 'power3.out', scrollTrigger: { trigger: s, start: 'top 88%' } })
      gsap.timeline({ scrollTrigger: { trigger: s, start: 'top 65%', end: 'bottom 65%', toggleClass: { targets: s, className: 'active' } } })
    })
  }, root.value)
})
</script>

<template>
  <section ref="root" id="proceso" class="process">
    <div class="pr-intro">
      <p class="eyebrow">Cómo trabajamos</p>
      <h2 class="title">De la idea a la <em>llave en mano</em></h2>
      <p class="lead">Un proceso claro en cinco etapas, con un solo equipo responsable de principio a fin.</p>
      <a href="#contacto" class="btn" @click.prevent="go('#contacto')">Iniciar mi proyecto</a>
    </div>

    <ol class="steps">
      <div class="rail"><div class="rail-fill"></div></div>
      <li class="step" v-for="(s, i) in steps" :key="s.t">
        <span class="dot"></span>
        <div class="card">
          <span class="num">0{{ i + 1 }}</span>
          <svg class="ico" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"><path :d="s.icon" /></svg>
          <div class="txt">
            <span class="tag">{{ s.tag }}</span>
            <h3>{{ s.t }}</h3>
            <p>{{ s.d }}</p>
          </div>
        </div>
      </li>
    </ol>
  </section>
</template>

<style scoped>
.process { display: grid; grid-template-columns: minmax(0, 5fr) minmax(0, 7fr); gap: clamp(2rem, 6vw, 6rem); align-items: start; }
.pr-intro { position: sticky; top: 7rem; }
.lead { margin: 1.5rem 0 2rem; color: var(--muted); max-width: 28rem; }
.steps { position: relative; list-style: none; padding: 0 0 0 2.2rem; margin: 0; display: grid; gap: 1.4rem; }
.rail { position: absolute; left: 0; top: 1rem; bottom: 1rem; width: 2px; background: var(--line); }
.rail-fill { height: 100%; background: linear-gradient(var(--gold), var(--gold-2)); transform-origin: top; }
.step { position: relative; }
.dot { position: absolute; left: calc(-2.2rem - 6px); top: 2rem; width: 14px; height: 14px; border-radius: 50%; background: var(--bg); border: 2px solid var(--gold); transition: background .4s, box-shadow .4s; z-index: 1; }
.step.active .dot { background: var(--gold); box-shadow: 0 0 0 8px rgba(212, 166, 58, .2); }
.card { position: relative; display: flex; align-items: center; gap: 1.4rem; padding: 1.5rem 1.8rem; border: 1px solid var(--line); border-radius: 1.2rem; background: var(--bg-2); overflow: hidden; opacity: .6; transition: opacity .5s, border-color .4s, transform .4s, box-shadow .4s; }
.step.active .card { opacity: 1; }
.card:hover { opacity: 1; border-color: var(--gold); transform: translateX(6px); box-shadow: 0 18px 50px -24px rgba(212, 166, 58, .5); }
.num { position: absolute; right: 1.2rem; top: .4rem; font-family: var(--font-display); font-size: 4rem; font-weight: 700; line-height: 1; color: rgba(212, 166, 58, .1); pointer-events: none; }
.ico { flex: none; width: 3.2rem; height: 3.2rem; padding: .8rem; border-radius: 50%; color: var(--gold); background: rgba(212, 166, 58, .1); border: 1px solid rgba(212, 166, 58, .3); }
.tag { font-size: .68rem; letter-spacing: .16em; text-transform: uppercase; color: var(--gold); }
.card h3 { font-family: var(--font-display); font-size: 1.4rem; margin: .2rem 0 .3rem; }
.card p { color: var(--muted); margin: 0; }

@media (max-width: 900px) {
  .process { grid-template-columns: 1fr; }
  .pr-intro { position: static; }
  .card { padding: 1.2rem; gap: 1rem; }
  .num { font-size: 3rem; }
}
</style>
