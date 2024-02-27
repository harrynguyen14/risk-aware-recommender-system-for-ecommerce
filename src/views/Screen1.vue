<!-- Screen1.vue -->
<template>
    <div>
        <movie-search @search="searchMovies"></movie-search>
        <div class="movie-container">
            <movie-card v-for="movie in filteredMovies" :key="movie.id" :movie="movie"></movie-card>
        </div>
        <add-movie @add="addMovie"></add-movie>
        <recommended-movies :movies="recommendedMovies"></recommended-movies>
    </div>
</template>
  
<script>
import MovieSearch from '@/components/MovieSearch.vue';
import MovieCard from '@/components/MovieCard.vue';
import AddMovie from '@/components/AddMovie.vue';
import RecommendedMovies from '@/components/RecommendedMovies.vue';
import moviesData from '@/movies.json';

export default {
    name: 'Screen1',
    components: {
        MovieSearch,
        MovieCard,
        AddMovie,
        RecommendedMovies
    },
    data() {
        return {
            movies: [],
            recommendedMovies: [],
            searchQuery: ''
        };
    },
    mounted() {
        // Load movie data when component is mounted
        this.movies = moviesData.movies;
    },
    computed: {
        filteredMovies() {
            // Filter movies based on search query
            return this.movies.filter(movie => {
                return movie.name.toLowerCase().includes(this.searchQuery.toLowerCase());
            });
        }
    },
    methods: {
        searchMovies(query) {
            this.searchQuery = query;
        },
        addMovie(newMovie) {
            // Generate unique ID for new movie
            const id = this.movies.length + 1;
            // Add new movie to the list
            this.movies.push({
                id,
                image: newMovie.poster,
                name: newMovie.title,
                rating: parseFloat(newMovie.rating),
                // Assuming other movie properties are not required for now
            });
        }
    }
}
</script>
  
<style>
.movie-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
}
</style>
  