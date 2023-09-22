<script setup>
import { reactive } from 'vue';
const estado = reactive({
  filtro: '+',
  campoA: '',
  campoB: '',
  resposta: 0
});


function filtrei(e) {
  estado.filtro = e.target.value;
  if (estado.campoA && estado.campoB) {
    calcular()
  }
}

function atualizarCampoA() {
  const campoA = document.getElementById('campoA').value;
  estado.campoA = campoA;
  if (estado.campoA && estado.campoB) {
    calcular()
  }
}

function atualizarCampoB() {
  const campoB = document.getElementById('campoB').value;
  estado.campoB = campoB;
  if (estado.campoA && estado.campoB) {
    calcular()
  }
}

function calcular() {
  const campoA = estado.campoA
  const campoB = estado.campoB
  const { filtro } = estado
  if (filtro === '+') {
    estado.resposta = parseFloat(campoA) + parseFloat(campoB)
  } else if (filtro === '*') {
    estado.resposta = parseFloat(campoA) * parseFloat(campoB)
  } else if (filtro === '/'){
    estado.resposta = parseFloat(campoA) / parseFloat(campoB)
  } else if (filtro === '-'){
    estado.resposta = parseFloat(campoA) - parseFloat(campoB)
  }
}

</script>

<template>
  <div class="fundo">
    <div class="card">
      <form card__form>
        <input @keyup="atualizarCampoA" type="number"  id="campoA" placeholder="Insira um valor" required>
        <input @keyup="atualizarCampoB" type="number"  id="campoB" placeholder="Insira outro valor" required>
      </form>
      <select @change="filtrei"  id="selectFiltro">
      <option value="+">Adição</option>
      <option value="-">Subtração</option>
      <option value="/">Divisão</option>
      <option value="*">Multiplicação</option>
    </select>
    <span>{{ `${estado.campoA} ${estado.filtro} ${estado.campoB} = ${estado.resposta}`}}</span>
    </div>
  </div>
</template>

<style scoped>
.fundo {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  background-image: linear-gradient(120deg, blue, black);
}

.card {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: rgba(80, 0, 0, 0.952);
  width: 300px;
  height: 300px;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.card form {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
  gap: 10px;
  width: 80%;
  margin-bottom: 10px;
}

.card form input {
  width: 100%;
  padding: 10px;
  text-align: center;
  outline-color: blue;
}

input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  -webkit-appearance: none;
  appearance: none;
  margin: 0;
}

select {
  width: 80%;
  text-align: center;
  margin-bottom: 10px;
  cursor: pointer;
}

span {
  background-color: white;
  width: 80%;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 5px;

}
</style>
