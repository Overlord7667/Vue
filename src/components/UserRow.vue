<template>
  <tr>
    <td class="username-cell">{{ user.username }}</td>
    <td class="email-cell">{{ user.email }}</td>
    <td class="date-cell">{{ new Date(user.registration_date).toLocaleDateString() }}</td>
    <td class="rating-cell">{{ user.rating }}</td>
    <td>
      <button class="delete-button" @click="$emit('deleteUser', user.id, user.username)">✖️</button> <!-- Изменен символ на тонкий крестик -->
    </td>
  </tr>
</template>

<script>
"use strict";
export default {
  props: {
    user: Object,
  },
};
</script>

<style>
.username-cell {
  font-size: 0.6rem; /* Уменьшенный размер шрифта для ячеек списка */
  color: #0CB4F1; /* Цвет имен пользователей изменен на #0CB4F1 */
}

.email-cell,
.date-cell,
.rating-cell {
  font-size: 0.6rem; /* Уменьшенный размер шрифта для ячеек списка */
  color: #ACACAC; /* Цвет для почты, даты и рейтинга изменен на #ACACAC */
}

.delete-button {
  background: transparent; /* Убираем задний фон */
  border: none; /* Убираем рамку */
  color: #000; /* Цвет крестика черный */
  font-size: 1rem; /* Размер шрифта для крестика */
  font-weight: 300; /* Тонкий шрифт */
  cursor: pointer; /* Указатель для интерактивной кнопки */
}

.delete-button:hover {
  opacity: 0.7; /* Эффект при наведении (необязательно) */
}
</style>