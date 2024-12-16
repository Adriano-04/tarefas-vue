<script setup>
import { reactive } from 'vue';


  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: [
      {
        titulo: 'Tarefa',
        finalizada: true,
      },
      {
        titulo: 'Estudar',
        finalizada: false,
      }
    ]
  })

  const getTarefasPedentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }

  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }

const getFiltro = () => {
  const { filtro} = estado

  switch (filtro) {
    case 'pendentes':
      return getTarefasPedentes();
    case 'finalizadas':
      return getTarefasFinalizadas();
    default:
      return estado.tarefas
  }
}

const cadastrarTarefa = () => {
  const novaTarefa = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  }

  estado.tarefas.push(novaTarefa);
  estado.tarefaTemp = ''
}
</script>

<template>
  <div class="container">
    <header class="p-5 mt-4 mb-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{ getTarefasPedentes().length }} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="cadastrarTarefa">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" type="text" class="form-control" placeholder="Descrição da nova tarefa">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change='evento => estado.filtro = evento.target.value' class="form-control">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Tarefas pendentes</option>
            <option value="finalizadas">Tarefas finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getFiltro()">
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" type="checkbox" :id="tarefa.titulo">
        <label :class=" { done: tarefa.finalizada }" :for="tarefa.titulo" class="ms-4">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>

  .done {
    text-decoration: line-through;
  }
</style>
