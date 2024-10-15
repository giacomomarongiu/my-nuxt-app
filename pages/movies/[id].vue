<script setup lang="ts">
const route = useRoute();

const { data } = await useFetch(
    `https://www.omdbapi.com/?apikey=ca1ac0be&i=${route.params.id}`
    , {
      pick:["Plot","Title","Error"],
      key: `movies/${route.params.id}`,

});

if(data.value.Error === "Incorrect IMDb ID.") {
  showError({statusCode: 404, message: "Movie not found!"});
}
</script>

<template>
<h1>{{data}}</h1>
</template>

<style scoped>

</style>