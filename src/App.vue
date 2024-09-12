<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Form from './components/Form.vue';
import TaskList from './components/TaskList.vue';


  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: [
      {
        titulo: 'Estudar ES6',
        finalizada: false,
      },
      {
        titulo: 'Estudar SASS',
        finalizada: false,
      },
      {
        titulo: 'Ir para a academia',
        finalizada: true,
      }
    ]
  })

  const getTarefasPen = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada )
  }

  const getTarefasFin = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada )
  }

  const getTarefasFil = () => {
    const {filtro} = estado;

    switch (filtro) {
      case 'pendentes':
        return getTarefasPen();
      case 'finalizadas':
        return getTarefasFin();
      default:
        return estado.tarefas;
    }
  }

  const cadastrarTarefa = () => {
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false,
    }
    estado.tarefas.push(tarefaNova);
    estado.tarefaTemp = '';
  }
</script>

<template>
<div class="container">
  <Cabecalho :tarefas-pendentes="getTarefasPen().length"/>
  <Form :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp = "estado.tarefaTemp" :edit-task-temp="evento => estado.tarefaTemp = evento.target.value" :cadastrar-tarefa="cadastrarTarefa"/>
  <TaskList :tarefas="getTarefasFil()" />


</div>
</template>


