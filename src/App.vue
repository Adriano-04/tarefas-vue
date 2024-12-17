<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';

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
    <Cabecalho :tarefas-pendentes="getTarefasPedentes()"/>
    <Formulario :troca-filtro="evento => estado.filtro = evento.target.value" :cadastrar-tarefa="cadastrarTarefa" :tarefa-temp="estado.tarefaTemp" :editar-tarefa="evento => estado.tarefaTemp = evento.target.value" />
    <ListaDeTarefas :tarefas="getFiltro()" />


  </div>
</template>

<style scoped>

  .done {
    text-decoration: line-through;
  }
</style>
