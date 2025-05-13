<template>
  <Header :scores="scores" />
  <div class="wrapper">
    <div class="container">
      <h1 class="title">Elige tu jugada</h1>

      <div class="selector">
        <label for="rondas">Mejor de:</label>
        <select id="rondas" v-model="selectedRounds">
          <option value="3">3 rondas</option>
          <option value="5">5 rondas</option>
          <option value="7">7 rondas</option>
        </select>
      </div>

      <div class="jugadas">
        <div class="botones bot-carrusel">
          <button v-for="jugada in jugadas" :key="jugada" @click="calcularResultado(jugada)">
            {{ icono(jugada) }}
          </button>
        </div>
      </div>

      <div class="reiniciar">
        <button @click="reiniciar">Reiniciar Juego</button>
      </div>
    </div>
  </div>
  <Footer />
</template>

<script setup>
import { reactive, ref } from 'vue'

const jugadas = ['piedra', 'papel', 'tijera']
const selectedRounds = ref(3)

const scores = reactive({
  usuario: 0,
  empates: 0,
  computadora: 0,
})

function icono(jugada) {
  return jugada === 'piedra' ? '✊' : jugada === 'papel' ? '✋' : '✌️'
}

function calcularResultado(jugadaDeUsuario) {
  const jugadaDeComputadora = calcularJugadaComputadora()
  const resultado = elegirGanador(jugadaDeUsuario, jugadaDeComputadora)

  const iconoUsuario = icono(jugadaDeUsuario)
  const iconoPC = icono(jugadaDeComputadora)

  if (resultado === 'Empate') {
    toast.info(`¡Empate! Ambos eligieron ${iconoUsuario}`, {
      icon: '🤝',
    })
  } else if (resultado === 'Usuario gana') {
    toast.success(`¡Ganaste! Jugaste: ${iconoUsuario} | La Computadora: ${iconoPC}`, {
      icon: '🎉',
    })
  } else {
    toast.warning(`¡Perdiste! Jugaste: ${iconoUsuario} | La Computadora: ${iconoPC}`, {
      icon: '😞',
    })
  }

  if (scores.usuario >= selectedRounds.value) {
    toast.success('¡Felicidades! Has ganado el juego.', {
      duration: 5000,
      position: 'top-left',
      icon: '🏆',
    })
    reiniciar()
  } 
  
  if (scores.computadora >= selectedRounds.value) {
    toast.error('¡La computadora ha ganado el juego!', {
      duration: 5000,
      position: 'top-left',
      icon: '💀',
    })
    reiniciar()
  }

  // if (elegirGanadorConstante === 'Empate') {
  //   console.log('¡Empate Técnico! Ambos eligieron:', jugadaDeUsuario)
  //   // alert('¡Empate! Ambos eligieron la misma jugada: ' + jugadaDeUsuario)
  // } else if(elegirGanadorConstante === 'Usuario gana'){
  //   console.log('¡Has ganado! Felicitaciones, tu jugada fue:', jugadaDeUsuario, "y la computadora eligió:", jugadaDeComputadora)
  //   // alert('¡Ganaste! Tu jugada fue: ' + jugadaDeUsuario + " y la computadora eligió: " + jugadaDeComputadora)
  // } else {
  //   console.log('¡Perdiste! Qué lástima, tu jugada fue:', jugadaDeUsuario, "y la computadora eligió:", jugadaDeComputadora)
  //   // alert('¡Perdiste! Tu jugada fue: ' + jugadaDeUsuario + " y la computadora eligió: " + jugadaDeComputadora)
  // }
}

function calcularJugadaComputadora() {
  const randomIndex = Math.floor(Math.random() * jugadas.length)
  return jugadas[randomIndex]
}

function elegirGanador(usuario, computadora) {
  if (usuario === computadora) {
    scores.empates++
    return 'Empate'
  } else if (
    (usuario === 'piedra' && computadora === 'tijera') ||
    (usuario === 'papel' && computadora === 'piedra') ||
    (usuario === 'tijera' && computadora === 'papel')
  ) {
    scores.usuario++
    return 'Usuario gana'
  } else {
    scores.computadora++
    return 'Computadora gana'
  }
}

function reiniciar() {
  scores.usuario = 0
  scores.empates = 0
  scores.computadora = 0
}

const toast = useNuxtApp().$toast;

import Footer from '~/components/footer.vue';  // Importar el componente Footer
import Header from '~/components/header.vue';  // Importar el componente Header

</script>

<style>
body {
  margin: 0;
}

/* Contenedor del carrusel */
.bot-carrusel {
  display: flex;
  overflow: hidden; /* Oculta los botones que salen del contenedor */
  width: 100%; /* Ajusta el ancho del carrusel */
  position: relative;
}

.bot-carrusel button:hover {
  animation: botCarrusel 1s 1;
}

@keyframes botCarrusel {
  50% {
    transform: rotatey(180deg);
  }
}

.wrapper {
  height: 100vh;
  display: flex;
  /* justify-content: center; */
  align-items: center;
  background: #afafaf;
}
.container {
  max-width: 400px;
  margin: 0 auto;
  padding: 2rem;
  background: #f5f7fa;
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  text-align: center;
  font-family: sans-serif;
}

.title {
  font-size: 1.8rem;
  font-weight: bold;
  color: #1e3a8a;
  margin-bottom: 1.5rem;
}

.scoreboard {
  display: flex;
  justify-content: space-between;
  background: #fff;
  border-radius: 10px;
  padding: 1rem;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
  margin-bottom: 1.5rem;
}

.scoreboard div {
  flex: 1;
  text-align: center;
}

.selector {
  margin-bottom: 1.5rem;
  text-align: left;
}

.selector label {
  margin-top: 1.5rem;
  display: block;
  font-weight: 600;
  margin-bottom: 0.5rem;
}

.selector select {
  width: 100%;
  padding: 0.5rem;
  font-size: 1rem;
}

.jugadas p {
  font-weight: 600;
  margin-bottom: 1rem;
}

.botones {
  display: flex;
  justify-content: center;
  gap: 1rem;
}

.botones button {
  width: 60px;
  height: 60px;
  font-size: 1.5rem;
  border-radius: 50%;
  border: none;
  background-color: #2563eb;
  color: white;
  cursor: pointer;
  transition: background 0.3s;
}

.botones button:hover {
  background-color: #1d4ed8;
}

.reiniciar button {
  background: #dc2626;
  color: white;
  border: none;
  padding: 0.6rem 1.2rem;
  border-radius: 6px;
  font-weight: bold;
  cursor: pointer;
  margin-top: 1.5rem;
}

.reiniciar button:hover {
  background: #b91c1c;
}

</style>