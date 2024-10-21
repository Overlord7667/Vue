<template>
  <table class="user-table">
    <tbody>
      <UserRow
        v-for="user in users"
        :key="user.id"
        :user="user"
        @deleteUser="$emit('deleteUser', user.id)"
      />
    </tbody>
  </table>
</template>

<script>
"use strict";
import UserRow from './UserRow.vue';

export default {
  props: {
    users: Array,
  },
  components: {
    UserRow,
  },
  methods: {
    sort(field) {
      this.$emit('sort', field);
    },
  },
};
</script>

<style>
.user-table {
  width: 100%; /* Устанавливаем ширину таблицы на 100% контейнера */
  border-collapse: collapse; /* Убираем отступы между ячейками */
}

.header-cell {
  margin-right: 10px;
  font-size: 0.6rem;
  color: #ACACAC;
  cursor: pointer;
  text-align: left;
  padding: 10px;
}

.header-cell:hover {
  color: #000000;
}

.user-table tr {
  height: 40px;
}

.user-table td {
  padding: 10px;
}

.username-cell {
  font-weight: bold;
}
</style>