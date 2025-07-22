<template>
  <div class="modal">
    <div class="modal-box">
      <h3>Listado de Boletas</h3>
      <div class="tabla-wrapper" ref="tabla">
        <table class="tabla-boletas">
          <thead>
            <tr>
              <th>#</th>
              <th>Comprador</th>
              <th>Contacto</th>
              <th>Estado</th>
              <th>Pagado</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="b in boletas.filter(b => b.estado !== 'disponible')" :key="b.numero">
              <td>{{ b.numero }}</td>
              <td>{{ b.comprador }}</td>
              <td>{{ b.contacto }}</td>
              <td>
                <span :class="'estado-tag ' + b.estado">{{ b.estado }}</span>
              </td>
              <td>${{ b.pagado }}</td>
            </tr>
          </tbody>
        </table>
      </div>

      <div class="acciones-tabla">
        <button class="btn" @click="descargarPDF">Descargar PDF</button>
        <button class="btn" @click="$emit('cerrar')">Cerrar</button>
      </div>
    </div>
  </div>
</template>


<script setup>
import { ref } from 'vue'
import html2pdf from 'html2pdf.js'

const props = defineProps(['boletas'])
const tabla = ref(null)

function descargarPDF() {
  html2pdf().from(tabla.value).save('boletas.pdf')
}
</script>
