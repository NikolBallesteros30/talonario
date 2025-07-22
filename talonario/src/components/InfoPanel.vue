<template>
  <div class="panel">
    <p>🏆 {{ config.premio }}</p>
    <p>💲 {{ config.valor }}</p>
    <p>🏛️ {{ config.loteria }}</p>
    <p>📅 {{ config.fecha }}</p>
    <button @click="$emit('editar')">Editar</button>
  </div>
</template>

<script setup>
defineProps(['config'])
defineEmits(['editar'])
</script>
