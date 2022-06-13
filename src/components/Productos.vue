<template>
  <div class="container mb-5">
    <h1 class="text-center mb-5">Peliculas en cartelera</h1>
    <div class="row justify-content-center">
      <div
        class="card text-white bg-dark  col-12 col-sm-3 m-4 shadow-lg p-3 mb-5  rounded "
        v-for="(item, index) in result"
        :key="index"
      >
        <img
          class="card-img-top"
          v-bind:src="item.poster_path"
          v-bind:alt="item.title"
        />
 
        <div class="card-body">
          <h5 class="card-title">{{ item.title }}</h5>
          <p class="card-text">Titulo Original: {{ item.original_title }}</p>
          <p class="card-text">Descripcion: {{ item.overview }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// Axios
// https://codingpotions.com/vue-axios
// https://es.vuejs.org/v2/guide/list.html
// Cotenido dinamico v-bind
// https://www.youtube.com/watch?v=B8rVlxQm8Cs
//Fetch Data
// https://youtu.be/7iDGJolHFmU
//import axios from "axios";
export default {
  /*   data: () => ({
    result: null,
  }),
  created() {
   axios.get("https://rickandmortyapi.com/api/character").then((result) => {
      this.result = result.data.results;
    });
  }, */
  data() {
    return {
      result: null,
    };
  },
   async created() {
    try {
      const res = await fetch("servicios/api.json");
      const data = await res.json();
      this.result = data.results;
    } catch (error) {
      console.log(error.message);
    }
  },
};
</script>

<style></style>