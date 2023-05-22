<script setup lang="ts">
import { reactive } from "vue";

interface NewTask {
  title: string;
  done: boolean;
}

const state = reactive({
  filter: "all",
  tempTask: "",
  tasks: [
    {
      title: "Estudar ES6",
      done: false,
    },
    {
      title: "Estudar SASS",
      done: false,
    },
    {
      title: "Ir para academia",
      done: true,
    },
  ],
});

const pendingTasks = () => {
  return state.tasks.filter((task) => task.done === false);
};

const doneTasks = () => {
  return state.tasks.filter((task) => task.done === true);
};

const filteredTasks = () => {
  const { filter } = state;

  switch (filter) {
    case "pending":
      return pendingTasks();

    case "done":
      return doneTasks();

    default:
      return state.tasks;
  }
};

const addTask = () => {
  const newTask: NewTask = {
    title: state.tempTask,
    done: false,
  };

  state.tasks.push(newTask);

  state.tempTask = "";
};
</script>

<template>
  <div class="container">
    <header class="p-5 my-4 bg-light rounded-3">
      <h1 class="h1">Minhas tarefas</h1>
      <p>Você possui {{ pendingTasks().length }} tarefas pendentes</p>
    </header>

    <form @submit.prevent="addTask">
      <div class="row">
        <div class="col">
          <input
            type="text"
            placeholder="Digite aqui a descrição da tarefa."
            class="form-control"
            required
            @change="e => state.tempTask = (<HTMLInputElement>e.target).value"
            :value="state.tempTask"
          />
        </div>
        <div class="col-md-2">
          <button class="btn btn-primary" type="submit">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select
            @change="(e) => (state.filter = (<HTMLSelectElement>e.target).value)"
            class="form-control"
          >
            <option value="all">Todas tarefas</option>
            <option value="pending">Tarefas pendente</option>
            <option value="done">Tarefas finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tasks in filteredTasks()">
        <input
          type="checkbox"
          :checked="tasks.done"
          :id="tasks.title"
          @change="(e) => (tasks.done = (<HTMLInputElement>e.target).checked)"
        />
        <label :class="{ done: tasks.done }" class="ms-3" :id="tasks.title">{{
          tasks.title
        }}</label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
