<script setup>
import { onMounted, ref } from 'vue'
import gsap from 'gsap'

const root = ref(null)
const steps = [
  ['Consulta', 'Escuchamos tu idea, terreno y presupuesto.'],
  ['Diseño', 'Desarrollamos planos, renders y especificaciones.'],
  ['Construcción', 'Ejecutamos la obra con cronograma claro.'],
  ['Supervisión', 'Control de calidad constante en cada etapa.'],
  ['Entrega', 'Te entregamos tu espacio listo para habitar.'],
]

onMounted(() => {
  gsap.context(() => {
    gsap.fromTo('.rail-fill', { scaleY: 0 }, { scaleY: 1, ease: 'none', scrollTrigger: { trigger: '.steps', start: 'top 60%', end: 'bottom 60%', scrub: true } })
    gsap.utils.toArray('.step').forEach((s) =>
      gsap.from(s, { x: (i) => 0, opacity: 0, y: 60, duration: 0.9, ease: 'power3.out', scrollTrigger: { trigger: s, start: 'top 80%', toggleClass: { targets: s, className: 'active' } } }))
  }, root.value)
})
</script>

<template>
  <section ref="root" id="proceso" class="process">
    <p class="eyebrow">Cómo trabajamos</p>
    <h2 class="title">De la idea a la <em>llave en mano</em></h2>
    <div class="steps">
      <div class="rail"><div class="rail-fill"></div></div>
      <div class="step" v-for="(s, i) in steps" :key="s[0]">
        <span class="dot"></span>
        <b>0{{ i + 1 }}</b>
        <div><h3>{{ s[0] }}</h3><p>{{ s[1] }}</p></div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.steps { position: relative; margin: 4rem 0 0 1rem; display: grid; gap: 3.5rem; max-width: 46rem; }
.rail { position: absolute; left: 0; top: 0; bottom: 0; width: 2px; background: var(--line); }
.rail-fill { height: 100%; background: linear-gradient(var(--gold), var(--gold-2)); transform-origin: top; }
.step { position: relative; display: flex; gap: 1.6rem; padding-left: 2.5rem; align-items: flex-start; opacity: .55; transition: opacity .5s; }
.step.active { opacity: 1; }
.dot { position: absolute; left: -6px; top: .6rem; width: 14px; height: 14px; border-radius: 50%; background: var(--bg); border: 2px solid var(--gold); transition: background .4s, box-shadow .4s; }
.step.active .dot { background: var(--gold); box-shadow: 0 0 0 8px rgba(212, 166, 58, .2); }
.step b { font-family: var(--font-display); font-size: 2.4rem; color: var(--gold); line-height: 1; }
.step h3 { font-family: var(--font-display); font-size: 1.5rem; }
.step p { color: var(--muted); }
</style>
