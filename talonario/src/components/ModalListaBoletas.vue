<template>
  <div class="modal">
    <div class="modal-box">
      <h3>Listado de Boletas</h3>
      <table ref="tabla">
        <thead>
          <tr>
            <th>#</th><th>Comprador</th><th>Contacto</th><th>Estado</th><th>Pagado</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="b in boletas.filter(b => b.estado !== 'disponible')" :key="b.numero">
            <td>{{ b.numero }}</td>
            <td>{{ b.comprador }}</td>
            <td>{{ b.contacto }}</td>
            <td>{{ b.estado }}</td>
            <td>{{ b.pagado }}</td>
          </tr>
        </tbody>
      </table>
      <button @click="descargarPDF">Descargar PDF</button>
      <button @click="$emit('cerrar')">Cerrar</button>
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
