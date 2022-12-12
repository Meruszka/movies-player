<script setup>
import MovieList from './components/MovieList.vue';
</script>

<template>
  <main>
    <MovieList />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    justify-content: center;
    padding-right: calc(var(--section-gap) / 2);
  }

}
</style>
