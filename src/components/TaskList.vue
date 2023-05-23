<script lang="ts" setup>
const { filteredTasks, pendingTasks } = defineProps([
  "filteredTasks",
  "pendingTasks",
]);
</script>

<template>
  <ul class="list-group mt-4">
    <li
      v-if="pendingTasks.length > 0"
      class="list-group-item"
      v-for="tasks in filteredTasks"
    >
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

    <p v-else class="h4">Não há tarefas pendentes.</p>
  </ul>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
