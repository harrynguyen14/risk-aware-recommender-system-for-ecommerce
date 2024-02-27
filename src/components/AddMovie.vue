<!-- AddMovie.vue -->
<template>
    <div class="add-movie">
      <h2 class="section-title">Add New Movie</h2>
      <form @submit.prevent="add" class="add-movie-form">
        <input type="text" v-model="newMovie.title" placeholder="Movie Title" class="form-input">
        <input type="text" v-model="newMovie.poster" placeholder="Movie Poster URL" class="form-input">
        <input type="number" v-model.number="newMovie.rating" min="0" max="5" step="0.1" placeholder="Rating" class="form-input">
        <button type="submit" class="btn-primary">Add Movie</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    name: 'AddMovie',
    data() {
      return {
        newMovie: {
          title: '',
          poster: '',
          rating: 0
        }
      };
    },
    methods: {
      add() {
        if (!this.newMovie.title || !this.newMovie.poster || !this.newMovie.rating) {
          alert('Please fill in all fields.');
          return;
        }
        this.$emit('add', this.newMovie);
        this.newMovie = { title: '', poster: '', rating: 0 };
      }
    }
  }
  </script>
  
  <style scoped>
  .add-movie {
    background-color: #111;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
  }
  
  .section-title {
    color: #fff;
    font-size: 24px;
    margin-bottom: 20px;
  }
  
  .add-movie-form {
    display: flex;
    flex-direction: column;
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
  
  
  