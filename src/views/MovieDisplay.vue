<template>
    <div class="movie-display">
      <div class="movie-list">
        <div v-for="movie in movies" :key="movie.id" class="movie-card">
          <img :src="movie.image" :alt="movie.name" class="movie-poster">
          <div class="movie-details">
            <h2>{{ movie.name }}</h2>
            <p>Director: {{ movie.director }}</p>
            <p>Year: {{ movie.year }}</p>
            <p>Rating: {{ movie.rating }}</p>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'MovieDisplay',
    data() {
      return {
        movies: [
          {
            id: 1,
            image: "https://w7.pngwing.com/pngs/1010/160/png-transparent-woody-from-toy-story-toy-story-3-the-video-game-sheriff-woody-jessie-buzz-lightyear-toy-story-cowboy-cowboy-hat-cartoon-thumbnail.png",
            name: "Toy Story 3",
            director: "Lee Unkrich",
            year: 2010,
            rating: 4.5,
            color: "#f7f6d7"
          },
          {
            id: 2,
            image: "https://w7.pngwing.com/pngs/526/409/png-transparent-john-wick-film-director-english-dts-others-sound-film-1080p.png",
            name: "John Wick",
            director: "Chad Stahelski",
            year: 2014,
            rating: 5.0,
            color: "#f5d3e4"
          }
        ]
      };
    }
  }
  </script>
  
  <style scoped>
  .movie-display {
    padding: 20px;
  }
  
  .movie-list {
    display: flex;
    flex-wrap: wrap;
  }
  
  .movie-card {
    width: calc(50% - 20px);
    margin: 10px;
    background-color: #141414;
    border-radius: 8px;
    overflow: hidden;
  }
  
  .movie-poster {
    width: 100%;
    height: auto;
    border-top-left-radius: 8px;
    border-top-right-radius: 8px;
  }
  
  .movie-details {
    padding: 10px;
    color: #fff;
  }
  
  .movie-details h2 {
    margin-top: 0;
  }
  
  .movie-details p {
    margin: 5px 0;
  }
  </style>
  