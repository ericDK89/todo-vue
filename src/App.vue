<script setup lang="ts">
import { reactive } from "vue";
import Header from "./components/Header.vue";
import Form from "./components/Form.vue";
import TaskList from "./components/TaskList.vue";

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

const addTask = () => {
  const newTask: NewTask = {
    title: state.tempTask,
    done: false,
  };

  state.tasks.push(newTask);

  state.tempTask = "";
};

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
</script>

<template>
  <div class="container">
    <Header :pending-tasks="pendingTasks().length" />
    <Form
      :temp-task="state.tempTask"
      :edit-temp-task="(e: Event) => (state.tempTask = (e.target as HTMLInputElement).value)"
      :add-task="addTask"
      :change-filter="(e: Event) => (state.filter = (e.target as HTMLInputElement).value)"
    />
    <TaskList
      :filtered-tasks="filteredTasks()"
      :pending-tasks="pendingTasks()"
    />
  </div>
</template>

<style scoped></style>
