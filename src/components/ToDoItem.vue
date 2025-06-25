<template>
  <div class="task__item" >
    <div class="item checkbox">
      <label class="custom__checkbox">
        <input type="checkbox" v-model="task.completed" />
        <span class="checkmark"></span>
      </label>
    </div>
    <div class="item description">
      {{ task.description }}
    </div>
    <div class="item status">
      {{ task.completed ? "Выполнено" : "В работе" }}
    </div>
    <div class="item date">
      {{ formattedDate }}
    </div>
  </div>
</template>

<script setup>
import { computed, defineProps } from "vue";

const props = defineProps(["task"]);

const formattedDate = computed(() => {
  const date = new Date(props.task.date);
  return date.toLocaleDateString("ru-RU");
});
</script>

<style scoped>
.task__item {
  max-width: 1300px;
  display: flex;
  align-items: center;
  transition: background-color 0.2s ease, box-shadow 0.2s ease;
  border-bottom: 1px solid #eeebe9;
  border-top: 1px solid #eeebe9;
  padding: 21px 29px 21px 40px;
  height: 58px;
}

.task__item:hover {
  background-color: #f6f9ff;
  box-shadow: 0px 4px 4px 0px #00000040;
  cursor: pointer;
  height: 64px;
}

.item {
  text-align: left;
  font-family: "Vela Sans", sans-serif;
  font-size: 14px;
  font-weight: 400;
  white-space: nowrap;
}

.checkbox {
  width: 67px;
}

.description {
  width: 1045px;
  font-family: "Vela Sans", sans-serif;
  font-weight: 400;
  font-size: 14px;
  line-height: 132%;
  color: #16191d;
}

.status {
  width: 151px;
  color: v-bind("task.completed ? '#134EC1' : '#F89B11'");
  font-weight: 500;
  font-family: "Vela Sans", sans-serif;
  font-weight: 400;
  font-size: 14px;
  line-height: 132%;
}

.date {
  padding-left: 20px;
  font-family: "Vela Sans", sans-serif;
  font-weight: 400;
  font-size: 14px;
  line-height: 132%;
}

.custom__checkbox {
  position: relative;
  display: inline-block;
  width: 20px;
  height: 20px;
  cursor: pointer;
}

.custom__checkbox input {
  opacity: 0;
  width: 0;
  height: 0;
}

.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 20px;
  width: 20px;
  background-color: #fff;
  border: 2px solid #16191d;
  border-radius: 50%;
  transition: background-color 0.2s ease, border-color 0.2s ease;
}

.custom__checkbox input:checked ~ .checkmark {
  border-color: #134ec1;
}

.checkmark::after {
  content: "";
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  width: 12px;
  height: 12px;
  background-image: url("/done.svg");
  background-size: contain;
  background-repeat: no-repeat;
  display: none;
}

.custom__checkbox input:checked ~ .checkmark::after {
  display: block;
}
</style>
