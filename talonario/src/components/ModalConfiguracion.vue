<template>
  <div class="modal">
    <div class="modal-box">
      <h2>CONFIGURA TU TALONARIO</h2>
      <input v-model="premio" placeholder="Ingrese el premio de la rifa" />
      <input v-model="valor" placeholder="Ingrese valor de la boleta" />
      <select v-model="loteria">
        <option disabled value="">Seleccione la lotería</option>
        <option>La Perla</option>
        <option>Chance Millonario</option>
      </select>
      <select v-model="cantidadBoletas">
        <option disabled value="">Cantidad de Boletas</option>
        <option v-for="n in 200" :key="n">{{ n }}</option>
      </select>
      <input type="date" v-model="fecha" />
      <button @click="guardar">Guardar</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const premio = ref('')
const valor = ref('')
const loteria = ref('')
const cantidadBoletas = ref('')
const fecha = ref('')

const emit = defineEmits(['guardar'])

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
    fecha: fecha.value,
  })
}
</script>
