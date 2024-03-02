<template>
  <div id="app">
    <Navigation />
    <div class="screen-wrapper">
      <!-- Screen 1 -->
      <div class="screen">

        <div class="search-movie">
          <input type="text" v-model="searchQuery" placeholder="Search movies...">
        </div>

        <div class="movie-list">
          <MovieCard v-for="movie in filteredMovies" :key="movie.id" :movie="movie" />
        </div>

        <AddMovie />
      </div>

      <!-- Screen 2 -->
      <div class="screen">
        <RecommendedMovies />

        <FairnessChecker />
        <ParameterAdjuster />
      </div>
    </div>
  </div>
</template>

<script>
import AddMovie from '@/components/AddMovie.vue';
import RecommendedMovies from '@/components/RecommendedMovies.vue';
import FairnessChecker from '@/components/FairnessChecker.vue';
import ParameterAdjuster from '@/components/ParameterAdjuster.vue';
import MovieCard from '@/components/MovieCard.vue';
import Navigation from '@/components/Navigation.vue'; 
import axios from 'axios';

export default {
  name: 'App',
  components: {
    AddMovie,
    FairnessChecker,
    RecommendedMovies,
    ParameterAdjuster,
    MovieCard,
    Navigation 
  },
  data() {
    return {
      searchQuery: '',
      movies: []
    };
  },
  mounted: function () {
    axios.get("movies.json").then((res) => {
      this.movies = res.data.movies;
    });
  },
  computed: {
    filteredMovies() {
      return this.movies.filter(movie =>
        movie.name.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    }
  }
}
</script>

<style>
#app {
  font-family: Arial, sans-serif;
}

.screen-wrapper {
  display: flex;
}

.screen {
  flex: 1;
  padding: 20px;
}

.search-movie input[type="text"] {
  padding: 10px;
  margin-bottom: 20px;
  width: 100%;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.movie-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  grid-gap: 20px;
}

.movie-list img {
  width: 100%;
  height: auto;
  border-radius: 8px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
}

.add-movie,
.fairness-checker,
.recommended-movies,
.parameter-adjuster {
  background-color: #111;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
  margin-bottom: 20px;
}

.section-title {
  color: #fff;
  font-size: 24px;
  margin-bottom: 20px;
}

.form-input {
  padding: 10px;
  margin-bottom: 10px;
  border: none;
  border-radius: 4px;
}

.btn-primary {
  background-color: #e50914;
  color: #fff;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.btn-primary:hover {
  background-color: #d30813;
}
</style>
