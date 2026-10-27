<script setup>
import { onMounted, ref } from 'vue'
import gsap from 'gsap'

const root = ref(null)
const values = ['Compromiso', 'Calidad', 'Responsabilidad', 'Innovación', 'Transparencia']

onMounted(() => {
  gsap.context(() => {
    gsap.from('.ab-title .line-mask > span', { yPercent: 110, stagger: 0.12, duration: 1, ease: 'expo.out', scrollTrigger: { trigger: '.ab-title', start: 'top 80%' } })
    gsap.utils.toArray('[data-reveal]', root.value).forEach((el) =>
      gsap.to(el, { opacity: 1, y: 0, duration: 1, ease: 'power3.out', scrollTrigger: { trigger: el, start: 'top 88%' } }))
    gsap.to('.ab-frame', { clipPath: 'inset(0% 0% 0% 0%)', duration: 1.6, ease: 'expo.out', scrollTrigger: { trigger: '.ab-frame', start: 'top 80%' } })
    gsap.to('.ab-frame svg', { yPercent: -10, ease: 'none', scrollTrigger: { trigger: '.ab-frame', scrub: true } })
  }, root.value)
})
</script>

<template>
  <section ref="root" id="empresa" class="about">
    <div class="grid">
      <div class="ab-visual">
        <div class="ab-frame">
          <svg viewBox="0 0 400 500" preserveAspectRatio="xMidYMid slice">
            <defs><linearGradient id="ag" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#22345e" /><stop offset="1" stop-color="#0b1220" /></linearGradient>
              <pattern id="aw" width="14" height="18" patternUnits="userSpaceOnUse"><rect x="3" y="4" width="7" height="9" fill="#f3d27a" opacity=".5" /></pattern></defs>
            <rect width="400" height="560" fill="url(#ag)" />
            <circle cx="300" cy="110" r="46" fill="#d4a63a" opacity=".85" />
            <rect x="60" y="180" width="110" height="380" fill="#0f1830" /><rect x="60" y="180" width="110" height="380" fill="url(#aw)" />
            <rect x="190" y="90" width="90" height="470" fill="#141f3a" /><rect x="190" y="90" width="90" height="470" fill="url(#aw)" />
            <rect x="295" y="230" width="80" height="330" fill="#0f1830" /><rect x="295" y="230" width="80" height="330" fill="url(#aw)" />
            <line x1="235" y1="90" x2="235" y2="40" stroke="#d4a63a" stroke-width="2" />
          </svg>
        </div>
        <div class="ab-badge" data-reveal><b>360°</b><span>supervisión y calidad en cada proyecto</span></div>
      </div>

      <div class="ab-text">
        <p class="eyebrow">Nuestra empresa</p>
        <h2 class="title ab-title">
          <span class="line-mask"><span>¡Comprometidos</span></span>
          <span class="line-mask"><span>con tu <em>proyecto!</em></span></span>
        </h2>
        <p class="lead" data-reveal>Somos una empresa salvadoreña dedicada a la arquitectura, diseño, supervisión y consultoría de proyectos de construcción residenciales, de oficinas corporativas y comerciales.</p>

        <div class="mv">
          <article data-reveal>
            <h3>Misión</h3>
            <p>Trabajamos proyectos generando espacios que ayuden a solucionar y transformar los entornos, con compromiso y calidad.</p>
          </article>
          <article data-reveal>
            <h3>Visión</h3>
            <p>Ser una empresa líder en diseño, construcción, supervisión y consultoría en El Salvador y, con el tiempo, en Centroamérica.</p>
          </article>
        </div>

        <div class="vals" data-reveal>
          <span v-for="v in values" :key="v">{{ v }}</span>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.grid { display: grid; grid-template-columns: 1fr 1.1fr; gap: clamp(2rem, 6vw, 7rem); align-items: center; }
.ab-visual { position: relative; }
.ab-frame { aspect-ratio: 4/5; border-radius: 1.2rem; overflow: hidden; clip-path: inset(100% 0 0 0); border: 1px solid var(--line); }
.ab-frame svg { width: 100%; height: 115%; }
.ab-badge { position: absolute; right: -1.5rem; bottom: 2rem; background: var(--gold); color: #1a1305; padding: 1.2rem 1.6rem; border-radius: 1rem; max-width: 11rem; box-shadow: 0 20px 50px -15px rgba(0,0,0,.6); }
.ab-badge b { font-family: var(--font-display); font-size: 2.6rem; display: block; line-height: 1; }
.ab-badge span { font-size: .8rem; font-weight: 500; line-height: 1.3; display: block; margin-top: .3rem; }
.lead { margin: 1.8rem 0 2.2rem; color: var(--muted); font-size: 1.1rem; max-width: 36rem; }
.mv { display: grid; grid-template-columns: 1fr 1fr; gap: 1.2rem; }
.mv article { padding: 1.5rem; border: 1px solid var(--line); border-radius: 1rem; background: var(--bg-2); transition: border-color .4s, transform .4s; }
.mv article:hover { border-color: var(--gold); transform: translateY(-6px) !important; }
.mv h3 { font-family: var(--font-serif); font-size: 1.7rem; color: var(--gold-2); margin-bottom: .5rem; }
.mv p { color: var(--muted); font-size: .92rem; }
.vals { margin-top: 1.6rem; display: flex; flex-wrap: wrap; gap: .6rem; }
.vals span { padding: .5rem 1.1rem; border: 1px solid var(--line); border-radius: 999px; font-size: .82rem; transition: all .3s; }
.vals span:hover { background: var(--gold); color: #1a1305; border-color: var(--gold); }
@media (max-width: 900px) { .grid { grid-template-columns: 1fr; } .ab-badge { right: 1rem; } .mv { grid-template-columns: 1fr; } }
</style>
