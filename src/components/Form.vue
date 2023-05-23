<script setup lang="ts">
const { addTask, tempTask, changeFilter, editTempTask } = defineProps([
  "addTask",
  "tempTask",
  "changeFilter",
  "editTempTask",
]);
</script>

<template>
  <form @submit.prevent="addTask()">
    <div class="row">
      <div class="col">
        <input
          type="text"
          placeholder="Digite aqui a descrição da tarefa."
          class="form-control"
          required
          @change="editTempTask"
          :value="tempTask"
        />
      </div>
      <div class="col-md-2">
        <button class="btn btn-primary" type="submit">Cadastrar</button>
      </div>
      <div class="col-md-2">
        <select @change="changeFilter" class="form-control">
          <option value="all">Todas tarefas</option>
          <option value="pending">Tarefas pendente</option>
          <option value="done">Tarefas finalizadas</option>
        </select>
      </div>
    </div>
  </form>
</template>

<script scoped></script>
