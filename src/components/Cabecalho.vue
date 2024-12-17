<script setup>
    const props = defineProps(['tarefasPendentes']);
</script>

<template>
    <header class="p-5 mt-4 mb-4 bg-light rounded-3">
    <h1>Minhas tarefas</h1>
    <p>
      Você possui {{ props.tarefasPendentes.length }} tarefas pendentes
    </p>
  </header>
</template>