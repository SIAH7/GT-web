<script setup>
const items = ['Arquitectura', 'Diseño', 'Construcción', 'Supervisión', 'Consultoría', 'Residencial', 'Comercial', 'Institucional']
</script>

<template>
  <div class="marquee" aria-hidden="true">
    <div class="track">
      <span v-for="n in 2" :key="n" class="group">
        <span v-for="(it, i) in items" :key="i">{{ it }} <i>✦</i></span>
      </span>
    </div>
  </div>
</template>

<style scoped>
.marquee { overflow: hidden; border-block: 1px solid var(--line); padding: 1.6rem 0; background: var(--bg-2); }
.track { display: flex; width: max-content; animation: slide 32s linear infinite; }
.marquee:hover .track { animation-play-state: paused; }
.group { display: flex; gap: 2.5rem; padding-right: 2.5rem; font-family: var(--font-display); font-size: clamp(1.4rem, 3vw, 2.6rem); text-transform: uppercase; font-weight: 700; color: transparent; -webkit-text-stroke: 1px rgba(255, 255, 255, .35); white-space: nowrap; }
.group i { color: var(--gold); -webkit-text-stroke: 0; font-style: normal; margin-left: 2.5rem; }
.group span:hover { color: var(--gold-2); -webkit-text-stroke-color: var(--gold-2); }
@keyframes slide { to { transform: translateX(-50%); } }
</style>
