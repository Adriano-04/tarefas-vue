<script setup>
    const props = defineProps(['cadastrarTarefa','tarefaTemp','trocaFiltro','editarTarefa'])
</script>

<template>
    <form @submit.prevent="props.cadastrarTarefa">
    <div class="row">
      <div class="col">
        <input :value="props.tarefaTemp" @change="props.editarTarefa" type="text" class="form-control" placeholder="Descrição da nova tarefa">
      </div>
      <div class="col-md-2">
        <button type="submit" class="btn btn-primary">Cadastrar</button>
      </div>
      <div class="col-md-2">
        <select @change='props.trocaFiltro' class="form-control">
          <option value="todas">Todas tarefas</option>
          <option value="pendentes">Tarefas pendentes</option>
          <option value="finalizadas">Tarefas finalizadas</option>
        </select>
      </div>
    </div>
  </form>
</template>