<template>
  <div class="grid">
    <button
      v-for="boleta in boletas"
      :key="boleta.numero"
      :class="['boleta', boleta.estado]"
      @click="$emit('editar-boleta', boleta)"
    >
      {{ boleta.numero }}
    </button>
  </div>
</template>

<script setup>
defineProps(['boletas', 'cantidad'])
defineEmits(['editar-boleta'])
</script>
