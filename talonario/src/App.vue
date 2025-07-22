<template>
  <div>
    <h1 class="header">TALONARIO</h1>
    <ModalConfiguracion
      v-if="!configurado"
      @guardar="handleGuardarConfiguracion"
    />
    <div v-else class="layout">
      <!-- Panel izquierdo -->
      <div class="columna panel-izquierdo">
        <InfoPanel :config="config" @editar="configurado = false" />
      </div>

      <!-- Centro - Grilla de boletas -->
      <div class="columna panel-centro">
        <TalonarioGrid
          :cantidad="parseInt(config.cantidadBoletas)"
          :boletas="boletas"
          @editar-boleta="handleEditarBoleta"
        />
      </div>

      <!-- Panel derecho -->
      <div class="columna panel-derecho">
        <div class="acciones">
          <button class="btn" @click="mostrarListado = true">📋 LISTAR BOLETAS</button>

          <button class="btn" @click="configurado = false">⚙️ PERSONALIZAR</button>
        </div>
      </div>
    </div>

    <ModalEditarBoleta
      v-if="boletaSeleccionada"
      :boleta="boletaSeleccionada"
      @guardar="actualizarBoleta"
      @cerrar="boletaSeleccionada = null"
    />

    <ModalListaBoletas
      v-if="mostrarListado"
      :boletas="boletas"
      @cerrar="mostrarListado = false"
    />

    
  </div>
</template>


<script setup>
import { ref } from 'vue'
import ModalConfiguracion from './components/ModalConfiguracion.vue'
import InfoPanel from './components/InfoPanel.vue'
import TalonarioGrid from './components/TalonarioGrid.vue'
import ModalEditarBoleta from './components/ModalEditarBoleta.vue'
import ModalListaBoletas from './components/ModalListaBoletas.vue'

const configurado = ref(false)
const config = ref({})
const boletas = ref([])
const boletaSeleccionada = ref(null)
const mostrarListado = ref(false)

function handleGuardarConfiguracion(datos) {
  config.value = datos
  configurado.value = true
  boletas.value = Array.from({ length: parseInt(datos.cantidadBoletas) }, (_, i) => ({
    numero: i,
    estado: 'disponible',
    comprador: '',
    contacto: '',
    pagado: 0,
  }))
}

function handleEditarBoleta(boleta) {
  boletaSeleccionada.value = boleta
}

function actualizarBoleta(boletaActualizada) {
  const index = boletas.value.findIndex(b => b.numero === boletaActualizada.numero)
  boletas.value[index] = boletaActualizada
  boletaSeleccionada.value = null
}
</script>
