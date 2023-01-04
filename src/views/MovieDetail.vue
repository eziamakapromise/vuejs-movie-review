<template>
  <router-link to="/">
    <h1 class="back">
      <img
        src="https://cdn-icons-png.flaticon.com/512/189/189254.png"
        alt=""
      /></h1
  ></router-link>
  <div class="movie-detail">
    <h2>{{ movie.Title }}</h2>
    <p>{{ movie.Year }}</p>
    <img :src="movie.Poster" alt="Movie Poster" class="featured-img" />
    <p>{{ movie.Plot }}</p>
  </div>
</template>

<script>
import { ref, onBeforeMount } from "vue";
import { useRoute } from "vue-router";

export default {
  metaInfo: {
    title: `MRWA - {{movie.Title}}`,
  },
  setup() {
    const movie = ref({});
    const route = useRoute();

    onBeforeMount(() => {
      fetch(
        `http://www.omdbapi.com/?apikey=925cf660&i=${route.params.id}&plot=full`
      )
        .then((response) => response.json())
        .then((data) => {
          movie.value = data;
        });
    });

    return {
      movie,
    };
  },
};
</script>

<style scoped>
.back img {
  text-align: left;
  width: 100px;
  padding: 1em;
}
.movie-detail {
  padding: 16px;
}
h2 {
  color: #fff;
  font-size: 28px;
  font-weight: 600;
  margin-bottom: 16px;
  text-align: center;
}

.featured-img {
  display: block;
  max-width: 200px;
  margin-bottom: 16px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0 auto;
}

p {
  color: #fff;
  font-size: 18px;
  line-height: 1.4;
  text-align: center;
}
</style>
