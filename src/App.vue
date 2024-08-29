<script setup>
import { reactive } from 'vue';

  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: [{
      titulo: 'Estudar ES8',
      finalizada: false
    },
    {
      titulo: 'Estudar SASS',
      finalizada: false,
    },
    {
      titulo: 'Ir para academia',
      finalizada: true,
    }]
  })

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada === false)
  }

  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada === true)
  }

  const getTarefasFiltradas = () =>{
    const filtro = estado.filtro

    switch(filtro) {
      case'pendentes':
       return getTarefasPendentes()
      case'finalizadas':
        return getTarefasFinalizadas()
      default:
        return estado.tarefas
    }
  }

  const cadastraTarefa = () => {
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false
    }
    estado.tarefas.push(tarefaNova)
    estado.tarefaTemp = ''
  }

</script>

<template>
    <div class="container">
      <header class="p-5 mb-4 mt-4 bg-light rounded-3">
        <h1>To do list</h1>
        <p>
          Você possui {{ getTarefasPendentes().length }} tarefas pendentes
        </p>
      </header>
      <form @submit.prevent="cadastraTarefa()">
        <div class="row">
          <div class="col">
            <input :value="estado.tarefaTemp" @change="e => estado.tarefaTemp = e.target.value" required type="text" placeholder="Digite uma tarefa" class="form-control">
          </div>
          <div class="col-md-2">
            <button class="btn btn-primary">Cadastrar</button>
          </div>
          <div class="col-md-2">
            <select class="form-control" @change="e => estado.filtro = e.target.value">
              <option value="todas">Todas tarefas</option>
              <option value="pendentes">Todas pendentes</option>
              <option value="finalizadas">Todas finalizadas</option>
            </select>
          </div>
        </div>
      </form>
      <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
          <input @change="e => tarefa.finalizada = e.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
          <label :class="{ done: tarefa.finalizada == true}" :for="tarefa.titulo" class="ms-3">
            {{ tarefa.titulo }}
          </label>
        </li>
      </ul>
    </div>
</template>

<style scoped>
  .done{
    text-decoration: line-through;
  }
</style>
