<template>
  <div>
    <div v-if="showModal" class="modal-overlay">
      <div class="modal-box">
        <button
          @click="showModal = false"
          class="close"
          style="cursor: pointer"
        >
          x
        </button>
        <h1 class="text-modal">Please enter name of movie</h1>
        <button @click="showModal = false" class="close-2">sure</button>
      </div>
    </div>
  </div>
  <div class="home">
    <div class="feature-card">
      <img
        src="https://images.pexels.com/photos/265685/pexels-photo-265685.jpeg?auto=compress&cs=tinysrgb&w=600"
        alt="https://images.pexels.com/photos/265685/pexels-photo-265685.jpeg?auto=compress&cs=tinysrgb&w=600"
        class="featured-img"
      />
      <div class="detail-1">
        <h3>MeetLine Movies Review</h3>
        <p>Read about movies or series before watching or downloading .</p>
      </div>
    </div>
    <form @submit.prevent="SearchMovies()" class="search-box">
      <input
        type="text"
        placeholder="What are you looking for?"
        v-model="search"
      />
      <input type="submit" value="Search" />
    </form>

    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="Movie Poster" />
            <div class="type">{{ movie.Type }}</div>
          </div>
          <div class="detail">
            <p class="year">{{ movie.Year }}</p>
            <h3>{{ movie.Title }}</h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
// import env from "@/env.js";

export default {
  setup() {
    const search = ref("");
    const movies = ref([]);
    let showModal = ref(false);
    let SearchMovies = () => {
      if (search.value != "") {
        fetch(`http://www.omdbapi.com/?apikey=925cf660&s=${search.value}`)
          .then((response) => response.json())

          .then((data) => {
            movies.value = data.Search;
            search.value = "";
            console.log(movies);
          });
      } else {
        showModal.value = true;
      }
    };

    return {
      search,
      movies,
      SearchMovies,
      showModal,
    };
  },
};
</script>

<style scoped>
@media screen and (min-width: 1024px) {
  .home {
    margin-left: 20rem;
    margin-right: 20rem;
  }
}
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 10;
}

.modal-box {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: white;
  padding: 10px;
  border-radius: 5px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
}
.close {
  float: right;
  font-size: 2em;
  border: none;
  background: white;
  padding-right: 20px;
}
.close-2 {
  border: none;
  background: #3b8070;
  border-radius: 5px;
  padding: 10px 10px;
  text-align: center;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0 auto;
}
.text-modal {
  color: #42b883;
  font-size: 1em;
  text-align: center;
  padding: 2em;
  margin-top: 2em;
}
.feature-card {
  position: relative;
}

.featured-img {
  display: block;
  width: 100%;
  height: 450px;
  object-fit: cover;
  position: relative;
  z-index: 0;
}

.detail-1 {
  /* background-color: #496583; */
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.6);
  padding: 16px;
  z-index: 1;
}

.detail-1 p {
  color: #fff;
  text-align: center;
}
.detail-1 h3 {
  text-align: center;
  font-size: 1.5rem;
  font-weight: 700;
  color: #fff;
  margin-bottom: 16px;
}

.search-box {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 16px;
}
input {
  display: block;
  appearance: none;
  border: none;
  outline: none;
  background: none;
}
input[type="text"] {
  width: 100%;
  color: #fff;
  background-color: #496583;
  font-size: 20px;
  padding: 10px 16px;
  border-radius: 8px;
  margin-bottom: 15px;
  transition: 0.4s;
}

input[type="submit"] {
  width: 100%;
  max-width: 300px;
  background-color: #42b883;
  padding: 16px;
  border-radius: 8px;
  color: #fff;
  font-size: 20px;
  text-transform: uppercase;
  transition: 0.4s;
}
input:active {
  background-color: #3b8070;
}

.movies-list {
  display: flex;
  flex-wrap: wrap;
  margin: 0px 8px;
}
.movie {
  max-width: 50%;
  flex: 1 1 50%;
  padding: 16px 8px;
}
.movie-link {
  display: flex;
  flex-direction: column;
  height: 100%;
}
.product-image {
  position: relative;
  display: block;
}
.movies-list img {
  display: block;
  width: 100%;
  height: 275px;
  object-fit: cover;
}

.type {
  position: absolute;
  padding: 8px 16px;
  background-color: #42b883;
  color: #fff;
  bottom: 16px;
  left: 0px;
  text-transform: capitalize;
}

.detail {
  background-color: #496583;
  padding: 16px 8px;

  flex: 1 1 100%;
  border-radius: 0px 0px 8px 8px;
}
.year {
  color: #aaa;
  font-size: 14px;
}

.detail h3 {
  color: #fff;
  font-weight: 600;
  font-size: 14px;
}
</style>
