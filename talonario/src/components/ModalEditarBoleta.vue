<template>
  <div class="modal">
    <div class="modal-box">
      <h3>Editar Boleta #{{ boleta.numero }}</h3>
      <input v-model="comprador" placeholder="Nombre del comprador" />
      <input v-model="contacto" placeholder="Contacto" />
      <select v-model="estado">
        <option value="disponible">Disponible</option>
        <option value="apartado">Apartado</option>
        <option value="pagado">Pagado</option>
      </select>
      <input v-model="pagado" placeholder="Monto pagado" />
      <button @click="guardar">Guardar</button>
      <button @click="$emit('cerrar')">Cancelar</button>
    </div>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'
const props = defineProps(['boleta'])
const emit = defineEmits(['guardar', 'cerrar'])

const comprador = ref('')
const contacto = ref('')
const estado = ref('')
const pagado = ref('')

watch(() => props.boleta, (b) => {
  comprador.value = b.comprador
  contacto.value = b.contacto
  estado.value = b.estado
  pagado.value = b.pagado
}, { immediate: true })

function guardar() {
  emit('guardar', {
    ...props.boleta,
    comprador: comprador.value,
    contacto: contacto.value,
    estado: estado.value,
    pagado: pagado.value,
  })
}
</script>
