<template>
  <div class="modal">
    <div class="modal-box">
      <h3>Editar Boleta #{{ boleta.numero }}</h3>

      <div class="campo">
        <input v-model="comprador" placeholder="Nombre del comprador" />
      </div>

      <div class="campo">
        <input v-model="contacto" placeholder="Contacto" />
      </div>

      <div class="campo">
        <select class="select-estado" v-model="estado">
  <option value="disponible">Disponible</option>
  <option value="apartado">Apartado</option>
  <option value="pagado">Pagado</option>
</select>

      </div>

      <div class="campo">
        <input v-model="pagado" placeholder="Monto pagado" />
      </div>

      <div class="campo" style="display: flex; gap: 10px; justify-content: center;">
        <button class="btn" @click="guardar">Guardar</button>
        <button class="btn" @click="$emit('cerrar')">Cancelar</button>
      </div>
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
