<template>
  <div id="app">
    <div class="container" :class="{ 'blur-background': showModal }">
      <div class="top__content">
        <h1 class="title">To do list</h1>
        <button class="button__plus" @click="showModal = true">
          <img class="plus" src="/plus.svg" />
        </button>
      </div>
      <SearchAndSort v-model:search="searchText" v-model:sort="sortType" />
      <div class="table__header">
        <div class="header__item forcheckbox"></div>
        <div class="header__item description">Описание</div>
        <div class="header__item status">Статус</div>
        <div class="header__item date">Дата</div>
      </div>
      <TodoList :tasks="sortedTasks" @update-task="updateTask" />

    </div>

    <AddTaskModal
  v-if="showModal"
  @close="showModal = false"
  @add-task="addTask"
  ref="addTaskModal"
/>
  </div>
</template>

<script setup>
import { ref, computed, watch, nextTick, watchEffect } from "vue";
import TodoList from "./components/TodoList.vue";
import SearchAndSort from "./components/SearchAndSort.vue";
import AddTaskModal from "./components/AddTaskModal.vue";

const tasks = ref([]);
const searchText = ref("");
const sortType = ref("date");
const showModal = ref(false);
const addTaskModal = ref(null);

watch(showModal, (newVal) => {
  if (newVal) {
    nextTick(() => {
      addTaskModal.value?.focusInput();
    });
  }
});

watchEffect(() => {
  const saved = localStorage.getItem("tasks");
  if (saved) {
    tasks.value = JSON.parse(saved);
  }
});

watchEffect(() => {
  localStorage.setItem("tasks", JSON.stringify(tasks.value));
});

const filteredTasks = computed(() => {
  return tasks.value.filter((task) =>
    task.description.toLowerCase().includes(searchText.value.toLowerCase())
  );
});

const sortedTasks = computed(() => {
  let arr = [...filteredTasks.value];
  if (sortType.value === "date") {
    return arr.sort((a, b) => new Date(a.date) - new Date(b.date));
  } else if (sortType.value === "status") {
    return arr.sort((a, b) => a.completed - b.completed);
  }
  return arr;
});

function addTask(task) {
  tasks.value.push(task);
}
function updateTask(updatedTask) {
  const index = tasks.value.findIndex(t => t.id === updatedTask.id);
  if (index !== -1) {
    tasks.value.splice(index, 1, updatedTask);
  }
}
</script>
<TodoList :tasks="sortedTasks" @update-task="updateTask" />

<style scoped>
#app {
  width: 100%;
}

.container {
  max-width: 1300px;
  margin: 0 auto;
  width: 100%;
}

.blur-background {
  filter: blur(2px);
  pointer-events: none;
}

.blur-background * {
  pointer-events: auto;
}

.top__content {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 27px;
  margin-top: 100px;
  padding-left: 40px;
}

.button__plus {
  background-color: #d6dbeb;
  width: 40px;
  height: 40px;
  border: none;
  cursor: pointer;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
}
.plus {
  width: 20px;
  height: 20px;
}
.title {
  font-family: "Montserrat", sans-serif;
  font-size: 24px;
  font-weight: 700;
  line-height: 132%;
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal {
  background: white;
  padding: 20px;
  border-radius: 10px;
  min-width: 300px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  z-index: 1001;
}

.table__header {
  display: flex;
  margin-bottom: 16px;
}

.header__item {
  text-align: left;
  padding-left: 20px;
  font-family: "Vela Sans",sans-serif;
  font-size: 14px;
  font-weight: 400;
  line-height: 132%;
  color: #16191d;
}

.forcheckbox {
  width: 80px;
}

.description {
  width: 937px;
  border-left: 1px solid #c4c4c4;
  font-family: "Vela Sans", sans-serif;
  font-weight: 400;
  font-size: 14px;
  line-height: 132%;
}

.status {
  width: 151px;
  border-left: 1px solid #c4c4c4;
  font-family: "Vela Sans", sans-serif;
  font-weight: 400;
  font-size: 14px;
  line-height: 132%;
}

.date {
  width: 70px;
  border-left: 1px solid #c4c4c4;
  font-family: "Vela Sans", sans-serif;
  font-weight: 400;
  font-size: 14px;
  line-height: 132%;
}
</style>
