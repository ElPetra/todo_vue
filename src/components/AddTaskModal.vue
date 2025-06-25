<template>
  <div class="modal__overlay" @click="handleOverlayClick">
    <div class="modal" @click.stop>
      <div class="madal__header">
        <h2 class="modal__title">Создать новую задачу</h2>
        <button class="button__close" @click="$emit('close')">&times;</button>
      </div>

      <div class="modal__content">
        <label class="madal__label">
          Описание
          <input class="modal__input" v-model="description" placeholder="Введите описание" />
        </label>
      </div>

      <div class="actions">
        <button class="button__add" @click="save">Создать</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const description = ref("");
const completed = ref(false);
const date = ref(new Date().toISOString().split("T")[0]);

const emit = defineEmits(["add-task", "close"]);

function save() {
  if (!description.value.trim()) return;

  const task = {
    description: description.value,
    completed: completed.value,
    date: date.value,
  };

  emit("add-task", task);
  emit("close");
}
</script>

<style scoped>
.modal__overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal {
  background: white;
  padding: 40px;
  border-radius: 8px;
  max-width: 400px;
  width: 100%;
  height: 281px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.madal__header {
  display: flex;
  justify-content: space-between;
  gap: 62px;
}

.modal__title {
  font-family: "Montserrat", sans-serif;
  font-size: 18px;
  font-weight: 700;
  line-height: 132%;
  margin: 0 0 24px 0;
  color: #16191d;
}

.button__close {
  cursor: pointer;
  color: #fff;
  background-color: #314b99;
  border-radius: 5px;
  width: 22px;
  height: 22px;
  display: flex;
  justify-content: center;
  align-items: center;
  padding-bottom: 3px;
}

.modal__content input {
  height: 40px;
  width: 100%;
  padding: 11px 16px;
  margin-top: 2px;
  box-sizing: border-box;
  font-family: "Vela Sans";
}

.madal__label {
  font-family: "AGAvantGardeCyrBook";
  font-weight: 400;
  font-size: 14px;
  line-height: 100%;
}
.modal__input {
  max-width: 319px;
  width: 100%;
  padding: 11px 16px;
  margin-top: 5px;
  box-sizing: border-box;
  font-family: "AGAvantGardeCyrBook", sans-serif;
  color: #16191D;
  font-size: 14px;
  line-height: 132%;
  border: 1px solid #dde2e4;
  border-radius: 8px;
}
.modal__input::placeholder {
  color: #000000;
  opacity: 0.5;
  font-size: 14px;
  font-family: "Vela Sans", sans-serif;
  line-height: 132%;
  font-weight: 400;
}

::-webkit-input-placeholder {
  color: #000000;
}
::-moz-placeholder {
  color: #000000;
  opacity: 0.5;
}
:-ms-input-placeholder {
  color: #000000;
}
:-moz-placeholder {
  color: #000000;
  opacity: 0.5;
}
.actions {
  margin-top: 30px;
  text-align: center;
}

.actions button {
  padding: 12px 40px;
  font-size: 18px;
  cursor: pointer;
  border: none;
  background-color: #f0f5ff;
  color: #314b99;
}
.button__add {
  padding: 12px 40px;
  font-family: "Vela Sans", sans-serif;
  font-size: 18px;
  cursor: pointer;
  border: none;
  border-radius: 8px;
  background-color: #F0F5FF;
  color: #314b99;
  line-height: 132%;
}
</style>
