<script setup lang="ts">


const query = ref('batman'); // 1
const movies = ref([]); // 4
async function search() {
  console.log(query.value); // 2
  const {Search} = await $fetch(`https://www.omdbapi.com/?apikey=ca1ac0be&s=${query.value}`) // 3
  movies.value = Search; // 5
}
search(); // 6
</script>

<template>
  <form @submit.prevent="search()">
    <label for="search">Search for a movie</label>
    <input type="text" id="search" name="search" v-model="query" />
    <button>Search</button>
  </form>
  <ul style="display: flex; flex-wrap: wrap;gap:10px; list-style: none">
    <li v-for="movie in movies" :key="movie.imdbID">
      <NuxtLink :to="{ name:'movies-id', params:{ id: movie.imdbID}}">
        <img :src="movie.Poster" :alt="movie.title" />
      </NuxtLink>
    </li>
  </ul>
</template>

<style scoped></style>
