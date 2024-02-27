<!-- MovieSearch.vue -->
<template>
    <div class="movie-search">
      <input type="text" v-model="query" placeholder="Search for a movie" class="search-input">
      <button @click="search" class="search-btn">Search</button>
    </div>
  </template>
  
  <script>
  export default {
    name: 'MovieSearch',
    data() {
      return {
        query: ''
      };
    },
    methods: {
      search() {
        this.$emit('search', this.query);
      }
    }
  }
  </script>
  
  <style scoped>
  .movie-search {
    display: flex;
    align-items: center;
  }
  
  .search-input {
    flex: 1;
    padding: 10px;
    margin-right: 10px;
    border: none;
    border-radius: 4px;
  }
  
  .search-btn {
    background-color: #e50914;
    color: #fff;
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  .search-btn:hover {
    background-color: #d30813;
  }
  </style>
  