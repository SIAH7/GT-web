<script setup>
import { onMounted, ref, computed } from 'vue'
import gsap from 'gsap'

const root = ref(null)
const filter = ref('Todos')
const filters = ['Todos', 'Residencial', 'Comercial e Institucional']
// Proyectos de ejemplo: reemplazar por proyectos reales con fotografías
const projects = [
  { t: 'Residencial Alturas', c: 'Residencial', y: '2024', hue: 38, floors: [5, 9, 7, 11] },
  { t: 'Torre Corporativa Central', c: 'Comercial e Institucional', y: '2024', hue: 215, floors: [8, 14, 10, 6] },
  { t: 'Casa Mirador', c: 'Residencial', y: '2023', hue: 160, floors: [3, 5, 4, 3] },
  { t: 'Centro Comercial Plaza', c: 'Comercial e Institucional', y: '2023', hue: 280, floors: [4, 6, 5, 7] },
  { t: 'Condominio Los Pinos', c: 'Residencial', y: '2022', hue: 18, floors: [6, 8, 6, 9] },
  { t: 'Edificio Institucional', c: 'Comercial e Institucional', y: '2022', hue: 195, floors: [7, 10, 7, 5] },
]
const shown = computed(() => projects.filter((p) => filter.value === 'Todos' || p.c === filter.value))

function setFilter(f) {
  gsap.to('.pj', { opacity: 0, y: 20, duration: 0.25, stagger: 0.03, onComplete: () => {
    filter.value = f
    requestAnimationFrame(() => gsap.fromTo('.pj', { opacity: 0, y: 40, scale: 0.95 }, { opacity: 1, y: 0, scale: 1, stagger: 0.08, duration: 0.6, ease: 'power3.out' }))
  } })
}

onMounted(() => {
  gsap.context(() => {
    gsap.from('.pj-title .line-mask > span', { yPercent: 110, stagger: 0.12, duration: 1, ease: 'expo.out', scrollTrigger: { trigger: '.pj-title', start: 'top 80%' } })
    gsap.utils.toArray('.pj').forEach((el, i) =>
      gsap.from(el, { y: 100, opacity: 0, duration: 1, delay: (i % 3) * 0.1, ease: 'power3.out', scrollTrigger: { trigger: el, start: 'top 90%' } }))
  }, root.value)
})
</script>

<template>
  <section ref="root" id="proyectos" class="projects">
    <div class="head">
      <div>
        <p class="eyebrow">Proyectos</p>
        <h2 class="title pj-title">
          <span class="line-mask"><span>Obras que <em>dejan huella</em></span></span>
        </h2>
      </div>
      <div class="filters">
        <button v-for="f in filters" :key="f" :class="{ on: f === filter }" @click="setFilter(f)">{{ f }}</button>
      </div>
    </div>

    <div class="grid">
      <article v-for="p in shown" :key="p.t" class="pj" data-cursor="Ver">
        <div class="art" :style="{ '--h': p.hue }">
          <svg viewBox="0 0 200 140" preserveAspectRatio="xMidYMax slice">
            <rect v-for="(f, i) in p.floors" :key="i" class="bld" :x="14 + i * 46" :y="140 - f * 11" width="36" :height="f * 11" fill="rgba(255,255,255,.14)" stroke="rgba(255,255,255,.35)" />
            <g v-for="(f, i) in p.floors" :key="'w' + i" fill="rgba(255,255,255,.55)">
              <rect v-for="k in f - 1" :key="k" :x="20 + i * 46" :y="140 - f * 11 + k * 11 - 6" width="24" height="3" />
            </g>
          </svg>
        </div>
        <div class="meta"><span>{{ p.c }} · {{ p.y }}</span><h3>{{ p.t }}</h3></div>
        <span class="arrow">↗</span>
      </article>
    </div>
  </section>
</template>

<style scoped>
.head { display: flex; justify-content: space-between; align-items: flex-end; gap: 2rem; flex-wrap: wrap; margin-bottom: 3.5rem; }
.filters { display: flex; gap: .6rem; flex-wrap: wrap; }
.filters button { padding: .6rem 1.2rem; border: 1px solid var(--line); border-radius: 999px; font-size: .82rem; color: var(--muted); transition: all .3s; }
.filters button:hover, .filters button.on { background: var(--gold); color: #1a1305; border-color: var(--gold); }
.grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(min(100%, 340px), 1fr)); gap: 1.5rem; }
.pj { position: relative; border-radius: 1.2rem; overflow: hidden; border: 1px solid var(--line); background: var(--bg-2); }
.art { aspect-ratio: 10/8; background: linear-gradient(160deg, hsl(var(--h) 55% 32%), hsl(var(--h) 45% 10%)); overflow: hidden; }
.art svg { width: 100%; height: 100%; transition: transform .9s cubic-bezier(.2, .8, .2, 1); transform-origin: bottom; }
.pj:hover .art svg { transform: scale(1.14); }
.meta { padding: 1.3rem 1.5rem 1.6rem; }
.meta span { font-size: .72rem; letter-spacing: .16em; text-transform: uppercase; color: var(--gold); }
.meta h3 { font-family: var(--font-display); font-size: 1.3rem; margin-top: .3rem; }
.arrow { position: absolute; top: 1rem; right: 1rem; width: 2.8rem; height: 2.8rem; display: grid; place-items: center; border-radius: 50%; background: var(--gold); color: #1a1305; font-size: 1.2rem; transform: scale(0) rotate(-90deg); transition: transform .5s cubic-bezier(.3, 1.4, .4, 1); }
.pj:hover .arrow { transform: scale(1) rotate(0); }
</style>
