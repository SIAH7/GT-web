<script setup>
import { onMounted, ref, watch } from 'vue'
import gsap from 'gsap'

const props = defineProps({ ready: Boolean })
const scrolled = ref(false)
const open = ref(false)
const links = [
  ['Empresa', '#empresa'], ['Servicios', '#servicios'], ['Proyectos', '#proyectos'],
  ['GreenTowers', '#green'], ['Proceso', '#proceso'], ['Contacto', '#contacto'],
]

onMounted(() => {
  window.addEventListener('scroll', () => (scrolled.value = window.scrollY > 60), { passive: true })
})
watch(() => props.ready, (r) => r && gsap.from('.nav', { yPercent: -100, opacity: 0, duration: 1, ease: 'power3.out' }))

function go(href) {
  open.value = false
  window.__lenis?.scrollTo(href, { offset: -20, duration: 1.6 })
}
</script>

<template>
  <header class="nav" :class="{ scrolled, open }">
    <a href="#" class="brand" @click.prevent="go(0)">
      <svg width="30" height="30" viewBox="0 0 64 64"><path d="M8 56V32h12v24zM26 56V8h12v48zM44 56V22h12v34z" fill="#d4a63a"/></svg>
      <span>GOLDEN<b>TOWERS</b></span>
    </a>
    <nav>
      <a v-for="[n, h] in links" :key="h" :href="h" @click.prevent="go(h)">{{ n }}</a>
    </nav>
    <a href="#contacto" class="btn nav-cta" @click.prevent="go('#contacto')">Cotizar</a>
    <button class="burger" aria-label="Menú" @click="open = !open"><i></i><i></i></button>
  </header>
</template>

<style scoped>
.nav {
  position: fixed; top: 0; left: 0; right: 0; z-index: 200;
  display: flex; align-items: center; justify-content: space-between; gap: 2rem;
  padding: 1.4rem var(--pad); transition: background .4s, padding .4s, backdrop-filter .4s;
}
.nav.scrolled { background: rgba(8, 13, 24, 0.75); backdrop-filter: blur(14px); padding-block: 0.85rem; border-bottom: 1px solid var(--line); }
.brand { display: flex; align-items: center; gap: 0.7rem; font-family: var(--font-display); letter-spacing: 0.22em; font-size: 0.85rem; font-weight: 700; }
.brand b { color: var(--gold); margin-left: 0.4em; }
nav { display: flex; gap: 2.2rem; }
nav a { font-size: 0.85rem; color: var(--muted); position: relative; transition: color .3s; }
nav a::after { content: ''; position: absolute; left: 0; bottom: -6px; width: 100%; height: 1px; background: var(--gold); transform: scaleX(0); transform-origin: right; transition: transform .4s; }
nav a:hover { color: var(--text); }
nav a:hover::after { transform: scaleX(1); transform-origin: left; }
.nav-cta { padding: 0.7rem 1.4rem; font-size: 0.72rem; }
.burger { display: none; width: 40px; height: 40px; position: relative; z-index: 3; }
.burger i { position: absolute; left: 8px; right: 8px; height: 2px; background: var(--text); transition: transform .35s, top .35s; }
.burger i:first-child { top: 15px; } .burger i:last-child { top: 23px; }
.open .burger i:first-child { top: 19px; transform: rotate(45deg); }
.open .burger i:last-child { top: 19px; transform: rotate(-45deg); }

@media (max-width: 900px) {
  .nav-cta { display: none; }
  .burger { display: block; }
  nav {
    position: fixed; inset: 0; background: var(--bg); flex-direction: column; justify-content: center; align-items: center; gap: 1.6rem;
    clip-path: circle(0% at calc(100% - 3rem) 2.5rem); transition: clip-path .7s cubic-bezier(.7, 0, .2, 1); z-index: 2;
  }
  .open nav { clip-path: circle(150% at calc(100% - 3rem) 2.5rem); }
  nav a { font-family: var(--font-display); font-size: 2rem; color: var(--text); }
}
</style>
