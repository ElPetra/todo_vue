<template>
  <div class="search__sort">
    <div class="search__wrapper">
      <img src="/search.svg" />
      <input v-model="search" placeholder="Поиск Имени, статуса или даты" />
    </div>
    <div class="sort__wrapper">
      <span class="sort__title">Сортировать по:</span>
      <select class="sort__select" v-model="sort">
        <option value="date">Дата</option>
        <option value="status">Статус</option>
      </select>
    </div>
  </div>
</template>

<script setup>
import { defineModel } from "vue";

const search = defineModel("search");
const sort = defineModel("sort");
</script>

<style scoped>
.search__sort {
  display: flex;
  justify-content: space-between;
  gap: 10px;
  margin-bottom: 36px;
  padding-left: 40px;
}

.search__wrapper {
  display: flex;
  gap: 16px;
  align-items: center;
}
.sort__wrapper {
  width: 178px;
  display: flex;
  gap: 13px;
  align-items: center;
}

input {
  min-width: 220px;
}
select {
  font-size: 14px;
  border: none;
  width: 100%;
}
::placeholder {
  color: #c4c4c4;
  opacity: 1;
  font-size: 14px;
  font-family: "Vela Sans", sans-serif;
  line-height: 132%;
  font-weight: 400;
}

::-webkit-input-placeholder {
  color: #c4c4c4;
}
::-moz-placeholder {
  color: #c4c4c4;
  opacity: 1;
}
:-ms-input-placeholder {
  color: #c4c4c4;
}
:-moz-placeholder {
  color: #c4c4c4;
  opacity: 1;
}
.sort__title {
  width: 112px;
  white-space: nowrap;
  font-family: "Vela Sans";
  color: #16191d;
  font-weight: 400;
  font-size: 14px;
  line-height: 132%;
  text-shadow: 0 0 4px rgba(0, 0, 0, 0.25);
}
.sort__select {
  font-family: "Vela Sans";
  color: #16191d;
  font-weight: 400;
  font-size: 14px;
  line-height: 132%;
  text-shadow: 0 0 4px rgba(0, 0, 0, 0.25);
}
</style>
