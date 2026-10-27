<script setup>
import { onMounted, reactive, ref } from 'vue'
import gsap from 'gsap'

const root = ref(null)
const form = reactive({ nombre: '', tipo: 'Residencial', mensaje: '' })

function send() {
  const txt = `Hola Golden Towers, soy ${form.nombre}. Me interesa un proyecto ${form.tipo}. ${form.mensaje}`
  window.open(`https://wa.me/50369805859?text=${encodeURIComponent(txt)}`, '_blank')
}

onMounted(() => {
  gsap.context(() => {
    gsap.from('.ct-title .line-mask > span', { yPercent: 110, stagger: 0.12, duration: 1, ease: 'expo.out', scrollTrigger: { trigger: '.ct-title', start: 'top 80%' } })
    gsap.from('.form > *, .info > *', { y: 40, opacity: 0, stagger: 0.08, duration: 0.8, scrollTrigger: { trigger: '.wrap', start: 'top 75%' } })
  }, root.value)
})
</script>

<template>
  <section ref="root" id="contacto" class="contact">
    <p class="eyebrow">Contacto</p>
    <h2 class="title ct-title">
      <span class="line-mask"><span>Trabajemos juntos</span></span>
      <span class="line-mask"><span><em>tu proyecto</em></span></span>
    </h2>
    <div class="wrap">
      <form class="form" @submit.prevent="send">
        <input v-model="form.nombre" required placeholder="Tu nombre" />
        <select v-model="form.tipo">
          <option>Residencial</option><option>Comercial</option><option>Institucional</option><option>Consultoría</option>
        </select>
        <textarea v-model="form.mensaje" rows="4" placeholder="Cuéntanos sobre tu proyecto"></textarea>
        <button class="btn" type="submit" data-cursor="Enviar">Enviar por WhatsApp →</button>
      </form>
      <div class="info">
        <a href="https://wa.me/50369805859" target="_blank"><small>WhatsApp</small>6980 5859</a>
        <a href="https://instagram.com/goldentowers.sv" target="_blank"><small>Instagram</small>@goldentowers.sv</a>
        <a href="https://facebook.com/goldentowers.sv" target="_blank"><small>Facebook</small>goldentowers.sv</a>
      </div>
    </div>
  </section>
</template>

<style scoped>
.wrap { margin-top: 3.5rem; display: grid; grid-template-columns: 1.3fr 1fr; gap: clamp(2rem, 6vw, 6rem); }
.form { display: grid; gap: 1rem; }
input, select, textarea { width: 100%; padding: 1.1rem 1.3rem; background: var(--bg-2); border: 1px solid var(--line); border-radius: .9rem; color: var(--text); font: inherit; outline: none; transition: border-color .3s, box-shadow .3s; }
input:focus, select:focus, textarea:focus { border-color: var(--gold); box-shadow: 0 0 0 4px rgba(212, 166, 58, .15); }
.form .btn { justify-self: start; }
.info { display: grid; gap: 1rem; align-content: start; }
.info a { padding: 1.3rem 1.5rem; border: 1px solid var(--line); border-radius: 1rem; font-family: var(--font-display); font-size: 1.3rem; transition: all .4s; }
.info a small { display: block; font-family: var(--font-body); font-size: .72rem; letter-spacing: .2em; text-transform: uppercase; color: var(--gold); }
.info a:hover { border-color: var(--gold); background: var(--bg-2); transform: translateX(10px); }
@media (max-width: 800px) { .wrap { grid-template-columns: 1fr; } }
</style>
