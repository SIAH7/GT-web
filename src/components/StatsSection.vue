<script setup>
import { onMounted, ref } from 'vue'
import gsap from 'gsap'

const root = ref(null)
// Cifras ilustrativas: reemplazar por datos reales de la empresa
const stats = ref([
  { v: 0, to: 50, suf: '+', l: 'Proyectos entregados' },
  { v: 0, to: 12, suf: '', l: 'Años de experiencia' },
  { v: 0, to: 30, suf: '+', l: 'Clientes satisfechos' },
  { v: 0, to: 100, suf: '%', l: 'Compromiso' },
])

onMounted(() => {
  gsap.context(() => {
    stats.value.forEach((s) =>
      gsap.to(s, { v: s.to, duration: 2.2, ease: 'power2.out', scrollTrigger: { trigger: root.value, start: 'top 75%' } }))
    gsap.from('.stat', { y: 50, opacity: 0, stagger: 0.12, duration: 0.9, scrollTrigger: { trigger: root.value, start: 'top 80%' } })
  }, root.value)
})
</script>

<template>
  <section ref="root" class="stats">
    <div class="stat" v-for="s in stats" :key="s.l">
      <b>{{ Math.round(s.v) }}{{ s.suf }}</b>
      <span>{{ s.l }}</span>
    </div>
  </section>
</template>

<style scoped>
.stats { display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 2rem; background: linear-gradient(120deg, var(--gold), var(--gold-2)); color: #1a1305; padding-block: 4.5rem; }
.stat { text-align: center; }
.stat b { display: block; font-family: var(--font-display); font-size: clamp(2.8rem, 6vw, 5rem); line-height: 1; }
.stat span { font-weight: 500; font-size: .9rem; letter-spacing: .05em; }
</style>
