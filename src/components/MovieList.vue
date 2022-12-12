<script>
  import movies from '../assets/data/movies.js'
  import { ref } from 'vue';
  import VideoPlayer from './Player.vue';
  export default{
    components: { VideoPlayer },
    mounted() {
    },
    setup() {
        const movieList = ref([]);
        movieList.value = movies;
        return { movieList };
    },
    methods: {
        showDetails(movie, movies) {
          if(movies.filter(m => m.isShowed === true).length > 0) {
            movies.filter(m => m.isShowed === true && m.id !== movie.id).forEach(m => m.isShowed = false);
          }
          movie.isShowed = !movie.isShowed;
        }
    },
    
}
</script>

<template>
  Lista filmów
  <div class="movies-list">
    <div class="movie" v-for="movie in movieList" :key="movie.id">
      <div class="title">
        <h1>{{movie.title}}</h1>
        <h5>{{movie.duration}}</h5>
        <div class="arrow" @click="showDetails(movie, movieList)"></div>
      </div>
      <VideoPlayer v-if="movie.isShowed" :path="movie.path"/>
    </div>
  </div>
</template>

<style scoped>

.arrow{
  width: 10px; 
  height: 10px; 
  border-left: 1px solid black; 
  border-bottom: 1px solid black;
  transform: rotate(-135deg);
  margin: 10px;
}
.arrow:hover{
  cursor: pointer;
  transform: rotate(-45deg) scale(1.2);
}

.movie{
  width: 600px;
  margin: 10px;
  border: 1px solid black;
  padding: 10px;
}
</style>
