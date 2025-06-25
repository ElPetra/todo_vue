<template>
  <div class="tasks__list">
    <TodoItem v-for="task in tasks" :key="task.id" :task="task" />
  </div>
</template>

<script setup>
import TodoItem from './ToDoItem.vue'
defineProps(['tasks'])
</script>

<style scoped>
.tasks__list {
  margin-top: 10px;
  max-width: 1300px;
}
</style>