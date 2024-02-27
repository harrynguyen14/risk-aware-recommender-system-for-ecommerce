<!-- MovieCard.vue -->
<template>
    <div class="movie-card">
      <img :src="movie.poster" alt="Movie Poster">
      <h3>{{ movie.title }}</h3>
      <p>Rating: {{ movie.rating }}</p>
    </div>
  </template>
  
  <script>
  export default {
    name: 'MovieCard',
    props: {
      movie: {
        type: Object,
        required: true
      }
    }
  }
  </script>
  
  <style scoped>
  .movie-card {
    background-color: #222;
    color: #fff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s ease;
  }
  
  .movie-card img {
    width: 100%;
    border-radius: 4px;
  }
  
  .movie-card h3 {
    margin-top: 10px;
    font-size: 18px;
  }
  
  .movie-card p {
    margin-top: 5px;
    font-size: 14px;
  }
  </style>
  
  