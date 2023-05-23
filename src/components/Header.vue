<script setup lang="ts">
const { pendingTasks } = defineProps(["pendingTasks"]);
</script>

<template>
  <header class="p-5 my-4 bg-light rounded-3">
    <h1 class="h1">Minhas tarefas</h1>
    <p>Você possui {{ pendingTasks }} tarefas pendentes</p>
  </header>
</template>

<script scoped></script>
