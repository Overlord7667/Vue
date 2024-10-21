<template>
  <div class="sort-options">
    <span class="sort-label">Сортировка:</span>
    <button class="registration-button" @click="sortBy('registration_date')">Дата регистрации</button>
    <button class="rating-button" @click="sortBy('rating')">Рейтинг</button>
  </div>
</template>

<script>
"use strict";
export default {
  methods: {
    sortBy(field) {
      this.$emit('sort', field); // Передаем событие сортировки
    }
  }
};
</script>

<style scoped>
.sort-options {
  display: flex;
  align-items: center;
  margin-bottom: 10px; /* Отступ для разделения с таблицей */
  margin-top: 65px;
}

.sort-options .sort-label {
  margin-right: 10px;
  font-size: 0.6rem;
  color: #ACACAC;
}

.sort-options .registration-button {
  margin-right: 5px;
  cursor: pointer;
  padding: 5px 10px;
  border: none;
  border-radius: 4px;
  font-size: 0.6rem; /* Уменьшаем размер шрифта для кнопок */
  background: #F7F7F7;
}

.sort-options .rating-button {
  margin-right: 5px;
  cursor: pointer;
  padding: 5px 10px;
  border: none;
  border-radius: 4px;
  font-size: 0.6rem; /* Уменьшаем размер шрифта для кнопок */
  color: #ACACAC;
  background: #F7F7F7
}
</style>