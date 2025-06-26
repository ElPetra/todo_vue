<template>
  <div class="tasks__list">
    <TodoItem
  v-for="task in tasks"
  :key="task.id"
  :task="task"
  @update:task="$emit('update-task', $event)"
/>
  </div>
</template>

<script setup>
import TodoItem from './ToDoItem.vue'
defineProps(['tasks'])
defineEmits(['update-task'])

function handleUpdateTask(updatedTask) {
  emit('update-task', updatedTask)
}

function updateTask(updatedTask) {
  // Находим индекс задачи и обновляем
  const index = tasks.findIndex(t => t.id === updatedTask.id);
  if (index !== -1) {
    tasks.splice(index, 1, updatedTask);
  }
}
</script>


<style scoped>
.tasks__list {
  margin-top: 10px;
  max-width: 1300px;
}
</style>