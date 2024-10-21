<template>
  <div class="search-container">
    <div class="search-input-container">
      <span class="search-icon">🔍</span> <!-- Иконка лупы -->
      <input
        type="text"
        class="search-input"
        placeholder="Поиск пользователей..."
        v-model="searchQuery"
        @input="emitSearch"
      />
    </div>
    <button class="clear-filter-button" @click="clearSearch">Очистить фильтр</button>
  </div>
</template>

<script>
"use strict";
export default {
  data() {
    return {
      searchQuery: '',
    };
  },
  methods: {
    emitSearch() {
      this.$emit('search', this.searchQuery);
    },
    clearSearch() {
      this.searchQuery = '';
      this.emitSearch();
    },
  },
};
</script>

<style>
.search-container {
  margin-top: 20px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  background-color: #ffffff;
  border-radius: 8px;
  padding: 10px;
  box-shadow: 0px 15px 20px rgba(0, 0, 0, 0.2);
}

.search-input-container {
  position: relative;
  width: 80%;
}

.search-icon {
  position: absolute;
  left: 10px;
  top: 50%;
  transform: translateY(-50%);
  font-size: 20px;
}

.search-input {
  width: 100%;
  padding: 10px 10px 10px 40px;
  font-size: 16px;
  border: none;
  outline: none;
  background: #e6e5e5;
  border-radius: 5px;
}

.clear-filter-button {
  margin-top: 10px;
  padding: 10px 20px;
  font-size: 12px;
  border: none;
  border-radius: 5px;
  background-color: #ffffff;
  cursor: pointer;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  transition: background-color 0.3s;
}

.clear-filter-button:hover {
  background-color: #f0f0f0;
}
</style>