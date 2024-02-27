<!-- RecommendedMovies.vue -->
<template>
    <div class="recommended-movies">
      <h2 class="section-title">Recommended Movies</h2>
      <ul class="movie-list">
        <li v-for="movie in movies" :key="movie.id" class="movie-item">{{ movie.title }}</li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    name: 'RecommendedMovies',
    props: {
      movies: {
        type: Array,
        required: true
      }
    }
  }
  </script>
  
  <style scoped>
  .recommended-movies {
    background-color: #111;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
  }
  
  .section-title {
    color: #fff;
    font-size: 24px;
    margin-bottom: 10px;
  }
  
  .movie-list {
    list-style: none;
    padding: 0;
  }
  
  .movie-item {
    color: #fff;
    margin-bottom: 5px;
    font-size: 16px;
  }
  </style>
  
  