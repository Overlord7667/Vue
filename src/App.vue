<template>
  <div class="app">
    <div class="main-container">
      <h2 class="header">Список пользователей</h2>
      <SearchBar @search="handleSearch" />
      <SortOptions @sort="handleSort" />
      <div class="header-row">
        <table class="user-table">
          <thead>
            <tr>
              <th class="header-cell">Имя пользователя</th>
              <th class="header-cell">E-mail</th>
              <th class="header-cell">Дата регистрации</th>
              <th class="header-cell">Рейтинг</th>
              <th class="header-cell">Действия</th>
            </tr>
          </thead>
        </table>
      </div>
      <div class="scrollable-container">
        <UserTable
          :users="filteredUsers"
          @deleteUser="prepareDeleteUser"
        />
      </div>
      <UserModal
        :visible="isModalVisible"
        :username="usernameToDelete"
        @confirm="handleDeleteUser"
        @cancel="cancelDelete"
      />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar.vue';
import UserTable from './components/UserTable.vue';
import UserModal from './components/UserModal.vue'; // Импортируем модальное окно
import SortOptions from './components/SortOptions.vue'; // Импортируем новый компонент сортировки
"use strict";

export default {
  name: 'App',
  components: {
    SearchBar,
    UserTable,
    UserModal,
    SortOptions, // Регистрация компонента сортировки
  },
  data() {
    return {
      users: [],
      searchQuery: '',
      sortField: '',
      sortOrder: 'asc',
      isModalVisible: false, // Состояние видимости модального окна
      usernameToDelete: '', // Имя пользователя для удаления
      idToDelete: null, // ID пользователя для удаления
    };
  },
  computed: {
    filteredUsers() {
      return this.users
        .filter(user => {
          const regex = new RegExp(this.searchQuery, 'i');
          return user.username.match(regex) || user.email.match(regex);
        })
        .sort((a, b) => {
          if (this.sortField) {
            const modifier = this.sortOrder === 'asc' ? 1 : -1;
            if (this.sortField === 'registration_date') {
              return (new Date(a.registration_date) - new Date(b.registration_date)) * modifier;
            } else if (this.sortField === 'rating') {
              return (a.rating - b.rating) * modifier;
            }
          }
          return 0;
        });
    },
  },
  methods: {
    async fetchUsers() {
      const response = await axios.get('https://5ebbb8e5f2cfeb001697d05c.mockapi.io/users');
      this.users = response.data;
    },
    handleSearch(query) {
      this.searchQuery = query; // Обработка запроса поиска
    },
    handleSort(field) {
      if (this.sortField === field) {
        this.sortOrder = this.sortOrder === 'asc' ? 'desc' : 'asc';
      } else {
        this.sortField = field;
        this.sortOrder = 'asc';
      }
    },
    prepareDeleteUser(id, username) {
      this.usernameToDelete = username; // Устанавливаем имя пользователя для удаления
      this.idToDelete = id; // Устанавливаем ID пользователя для удаления
      this.isModalVisible = true; // Показываем модальное окно
    },
    handleDeleteUser() {
      this.users = this.users.filter(user => user.id !== this.idToDelete);
      this.isModalVisible = false; // Скрываем модальное окно после удаления
      this.usernameToDelete = ''; // Сбрасываем имя пользователя
      this.idToDelete = null; // Сбрасываем ID пользователя
    },
    cancelDelete() {
      this.isModalVisible = false; // Закрываем модальное окно без удаления
      this.usernameToDelete = ''; // Сбрасываем имя пользователя
      this.idToDelete = null; // Сбрасываем ID пользователя
    },
  },
  mounted() {
    this.fetchUsers();
  },
};
</script>

<style>
.app {
  background-color: #f0f0f0;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.main-container {
  width: 1000px;
  height: 647px;
  background-color: #fff;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
  padding: 20px;
  box-sizing: border-box;
}

.header {
  font-size: 1.4rem; /* Уменьшаем размер шрифта заголовка */
  font-weight: bold; /* Делаем заголовок жирным */
}

.header-row {
  position: sticky; /* Фиксируем заголовок */
  top: 0; /* Отступ от верхней части */
  background-color: #fff; /* Фоновый цвет для заголовка */
}

.scrollable-container {
  max-height: 290px; /* Максимальная высота контейнера для прокрутки */
  overflow-y: auto; /* Вертикальная прокрутка */
  margin-top: 10px;
}
</style>