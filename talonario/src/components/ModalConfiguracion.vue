<template>
  <div class="modal">
    <div class="modal-box">
      <div class="modal-header">
        <h2>CONFIGURA TU TALONARIO</h2>
        <button class="close-btn" @click="cerrar">×</button>
      </div>

      <div class="modal-body">
        <input v-model="premio" placeholder="Ingrese el premio de la rifa" />
        <input v-model="valor" placeholder="Ingrese valor de la boleta" />
        <select v-model="loteria">
          <option disabled value="">Seleccione la lotería</option>
          <option>La Perla</option>
          <option>Chance Millonario</option>
          <option>Cruz Roja</option>
          
        </select>
        <select v-model="cantidadBoletas">
          <option disabled value="">Cantidad de Boletas</option>
          <option v-for="n in 200" :key="n">{{ n }}</option>
        </select>
        <input type="date" v-model="fecha" />
        <button class="guardar-btn" @click="guardar">Guardar</button>
      </div>
    </div>
  </div>
</template>


<script setup>
import { ref } from 'vue'
const emit = defineEmits(['guardar'])

const premio = ref('')
const valor = ref('')
const loteria = ref('')
const cantidadBoletas = ref('')
const fecha = ref('')

function guardar() {
  if (!premio.value || !valor.value || !loteria.value || !cantidadBoletas.value || !fecha.value) {
    alert('Por favor complete todos los campos.')
    return
  }

  emit('guardar', {
    premio: premio.value,
    valor: valor.value,
    loteria: loteria.value,
    cantidadBoletas: cantidadBoletas.value,
    fecha: fecha.value
  })
}

function cerrar() {
  alert("No puedes cerrar este modal sin completar los datos.")
}

</script>
