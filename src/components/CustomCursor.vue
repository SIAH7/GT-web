<script setup>
import { onMounted, onBeforeUnmount, ref } from 'vue'
import gsap from 'gsap'

const dot = ref(null)
const ring = ref(null)
const label = ref('')
let off = []

onMounted(() => {
  if (!window.matchMedia('(hover: hover) and (pointer: fine)').matches) return
  document.body.classList.add('has-cursor')
  const dx = gsap.quickTo(dot.value, 'x', { duration: 0.1 })
  const dy = gsap.quickTo(dot.value, 'y', { duration: 0.1 })
  const rx = gsap.quickTo(ring.value, 'x', { duration: 0.45, ease: 'power3' })
  const ry = gsap.quickTo(ring.value, 'y', { duration: 0.45, ease: 'power3' })
  const move = (e) => { dx(e.clientX); dy(e.clientY); rx(e.clientX); ry(e.clientY) }
  const over = (e) => {
    const t = e.target.closest('[data-cursor], a, button')
    ring.value?.classList.toggle('big', !!t)
    label.value = t?.dataset?.cursor || ''
  }
  window.addEventListener('mousemove', move)
  window.addEventListener('mouseover', over)
  off = [() => window.removeEventListener('mousemove', move), () => window.removeEventListener('mouseover', over)]
})
onBeforeUnmount(() => off.forEach((f) => f()))
</script>

<template>
  <div ref="ring" class="c-ring"><span>{{ label }}</span></div>
  <div ref="dot" class="c-dot"></div>
</template>

<style scoped>
.c-dot, .c-ring { position: fixed; top: 0; left: 0; pointer-events: none; z-index: 500; translate: -50% -50%; }
.c-dot { width: 6px; height: 6px; border-radius: 50%; background: var(--gold-2); }
.c-ring {
  width: 38px; height: 38px; border-radius: 50%; border: 1px solid var(--gold);
  display: grid; place-items: center; transition: width .3s, height .3s, background .3s;
  font-family: var(--font-display); font-size: 0.65rem; letter-spacing: 0.1em; text-transform: uppercase; color: #1a1305;
}
.c-ring.big { width: 84px; height: 84px; background: rgba(212, 166, 58, 0.9); mix-blend-mode: normal; }
@media (hover: none), (pointer: coarse) { .c-dot, .c-ring { display: none; } }
</style>
