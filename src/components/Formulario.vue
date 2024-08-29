<script setup>
  const props = defineProps(['cadastraTarefa', 'tarefaTemp', 'trocarFiltro', 'editaTarefaTemp'])
</script>

<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
          <div class="col">
            <input :value="props.tarefaTemp" @change="props.editaTarefaTemp" required type="text" placeholder="Digite uma tarefa" class="form-control">
          </div>
          <div class="col-md-2">
            <button class="btn btn-primary">Cadastrar</button>
          </div>
          <div class="col-md-2">
            <select class="form-control" @change="props.trocarFiltro">
              <option value="todas">Todas tarefas</option>
              <option value="pendentes">Todas pendentes</option>
              <option value="finalizadas">Todas finalizadas</option>
            </select>
          </div>
        </div>
      </form>
</template>