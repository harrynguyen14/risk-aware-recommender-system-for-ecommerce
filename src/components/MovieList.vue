<!-- MovieList.vue -->
<template>
    <div>
      <MovieCard v-for="movie in movies" :key="movie.id" :movie="movie" />
    </div>
  </template>
  
  <script>
  import moviesData from '@/public/movies.json'; 
  import MovieCard from '@/components/MovieCard.vue';
  
  export default {
    components: {
      MovieCard
    },
    data() {
      return {
        movies: moviesData.movies
      };
    }
  }
  </script>
  