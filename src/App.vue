<template>
  <div id="app">
    <!-- Screen 1 -->
    <div v-if="currentScreen === 1">
      
      <div class="search-movie">
        <input type="text" v-model="searchQuery" placeholder="Search movies...">
      </div>
      
      <div class="movie-list">
        <MovieCard v-for="movie in filteredMovies" :key="movie.id" :movie="movie" />
      </div>
      
      <AddMovie />
      
      <RecommendedMovies />
    </div>

    <!-- Screen 2 -->
    <div v-else>
      
      <BiasChecker />
      
      <ParameterAdjuster />
    </div>
  </div>
</template>

<script>
import AddMovie from '@/components/AddMovie.vue';
import BiasChecker from '@/components/BiasChecker.vue';
import RecommendedMovies from '@/components/RecommendedMovies.vue';
import ParameterAdjuster from '@/components/ParameterAdjuster.vue';
import MovieCard from '@/components/MovieCard.vue';

export default {
  name: 'App',
  components: {
    AddMovie,
    BiasChecker,
    RecommendedMovies,
    ParameterAdjuster,
    MovieCard
  },
  data() {
    return {
      currentScreen: 1, 
      searchQuery: '',
      movies: []
    };
  },
  mounted: function () {
    axios
      .get("movies.json")
      .then((res) => {
        console.log(res.data)
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
.bias-checker,
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



