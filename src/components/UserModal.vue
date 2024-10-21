<template>
  <div class="modal-overlay" v-if="visible">
    <div class="modal-content">
      <p>Вы уверены, что хотите удалить пользователя {{ username }}?</p>
      <div class="button-container">
        <button class="confirm-button" @click="confirmDelete">Да</button>
        <button class="cancel-button" @click="$emit('cancel')">Нет</button>
      </div>
    </div>
  </div>
</template>

<script>
"use strict";
export default {
  name: 'UserModal',
  props: {
    visible: {
      type: Boolean,
      required: true,
    },
    username: {
      type: String,
      required: true,
    },
  },
  methods: {
    confirmDelete() {
      this.$emit('confirm'); // Уведомляем родительский компонент о подтверждении удаления
    }
  }
};
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 0.8rem;
}

.modal-content {
  background: #fff;
  padding: 20px;
  border-radius: 8px;
  text-align: center;
}

.button-container {
  display: flex; /* Устанавливаем flexbox для горизонтального расположения кнопок */
  justify-content: center; /* Центрируем кнопки по горизонтали */
}

.modal-content button {
  margin: 5px;
  width: 100px; /* Устанавливаем фиксированную ширину для кнопок */
  height: 30px; /* Увеличиваем высоту кнопок */
  border: none; /* Убираем рамку */
  border-radius: 5px; /* Добавляем закругление углов */
  cursor: pointer; /* Указатель для интерактивных кнопок */
  display: flex; /* Используем flexbox для центрирования текста */
  justify-content: center; /* Центрируем текст по горизонтали */
  align-items: center; /* Центрируем текст по вертикали */
}

.confirm-button {
  background-color: #E0E0E0; /* Цвет фона кнопки Да */
}

.cancel-button {
  background-color: #0CB4F1; /* Цвет фона кнопки Нет */
  color: #fff; /* Цвет текста кнопки Нет */
}

.modal-content button:hover {
  opacity: 0.8; /* Эффект при наведении (необязательно) */
}
</style>