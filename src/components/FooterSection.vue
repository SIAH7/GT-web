<template>
  <footer>
    <p class="big">GOLDEN TOWERS</p>
    <div class="row">
      <span>© {{ new Date().getFullYear() }} Golden Towers S.A. de C.V. · El Salvador</span>
      <span>Arquitectura · Diseño · Supervisión · Consultoría</span>
    </div>
  </footer>
</template>

<style scoped>
footer { padding: 4rem var(--pad) 2rem; border-top: 1px solid var(--line); overflow: hidden; }
.big { font-family: var(--font-display); font-weight: 800; font-size: clamp(2.5rem, 12.5vw, 12rem); line-height: .9; text-align: center; color: transparent; -webkit-text-stroke: 1px rgba(212, 166, 58, .5); transition: color .6s; }
.big:hover { color: var(--gold); }
.row { margin-top: 2.5rem; display: flex; justify-content: space-between; gap: 1rem; flex-wrap: wrap; color: var(--muted); font-size: .82rem; }
</style>
