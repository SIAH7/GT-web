<script setup>
import { onMounted, ref } from 'vue'
import gsap from 'gsap'

const emit = defineEmits(['done'])
const root = ref(null)
const count = ref(0)

onMounted(() => {
  const o = { v: 0 }
  const tl = gsap.timeline()
  tl.from('.pl-bar', { scaleY: 0, stagger: 0.12, duration: 0.7, ease: 'power3.out', transformOrigin: 'bottom' })
    .to(o, { v: 100, duration: 1.4, ease: 'power2.inOut', onUpdate: () => (count.value = Math.round(o.v)) }, 0)
    .to('.pl-inner', { opacity: 0, y: -30, duration: 0.5 })
    .to(root.value, { yPercent: -100, duration: 1, ease: 'expo.inOut', onStart: () => emit('done') })
    .set(root.value, { display: 'none' })
})
</script>

<template>
  <div ref="root" class="preloader">
    <div class="pl-inner">
      <div class="pl-towers">
        <span class="pl-bar" style="height: 46px"></span>
        <span class="pl-bar" style="height: 90px"></span>
        <span class="pl-bar" style="height: 64px"></span>
        <span class="pl-bar" style="height: 120px"></span>
      </div>
      <p class="pl-name">GOLDEN TOWERS</p>
      <p class="pl-count">{{ count }}%</p>
    </div>
  </div>
</template>

<style scoped>
.preloader { position: fixed; inset: 0; z-index: 1000; background: var(--bg); display: grid; place-items: center; }
.pl-inner { text-align: center; }
.pl-towers { display: flex; align-items: flex-end; gap: 8px; justify-content: center; height: 130px; }
.pl-bar { width: 26px; background: linear-gradient(to top, var(--gold), var(--gold-2)); border-radius: 2px 2px 0 0; }
.pl-name { margin-top: 1.5rem; font-family: var(--font-display); letter-spacing: 0.5em; font-size: 0.85rem; color: var(--muted); }
.pl-count { font-family: var(--font-display); font-size: 2.4rem; margin-top: 0.5rem; color: var(--gold-2); }
</style>
