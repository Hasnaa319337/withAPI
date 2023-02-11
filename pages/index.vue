<template>
  <section class="home">
    <!-- Hero section -->
    <hero />

    <!-- end hero -->

    <!-- start search -->

    <div class="container search">
      <input
        class="search-input"
        placeholder="search"
        name="search"
        v-model="searchInput"
      />
      <button @click="clearSearch" class="button" v-show="searchInput !== ''">
        clear search
      </button>
    </div>
    <!-- end search -->

    <!-- movies section -->
    <div class="movies container">
      <div class="movie-grid">
        <div class="movie" v-for="(item, index) in movies" :key="index" >
          <div class="movie-img">
            <img :src=" `https://image.tmdb.org/t/p/w500/${item.poster_path}` "/>
            <div class="review">{{ item.vote_average }}</div>
            <div class="overview">{{ item.overview }}</div>
          </div>

          <div class="info">
            <p class="title">{{ item.title }}</p>
            <p class="release">
              Released:
              {{
                new Date(item.release_date).toLocaleString('en-us', {
                  month: 'long',
                  day: 'numeric',
                  year: 'numeric',
                })
              }}
            </p>
            <nuxt-link
              class="button button-light"
              :to="{ name: 'movies-movieid', params:{ movieid: item.id } }"
              >Get More Info</nuxt-link
            >
          
          </div>
        </div>
      </div>
    </div>

    <!-- end movies section -->
  </section>
</template>
<script>
import Hero from "~/components/Hero";

export default {
  components: {
    Hero,
  },

  async asyncData({ $axios }) {
    const movies = await $axios.$get(
      `https://api.themoviedb.org/3/movie/now_playing?api_key=37ed43a4f8eaa2abd75f9283692947bc&language=en-US&page=1`
    );
    return {
      movies: movies.results,
    };

  },

  data() {
    return {
      searchInput: "",
      searchedMovies: [],
    };
  },

  methods: {
    clearSearch() {
      this.searchInput = "";
      this.searchedMovies = [];
    },
  },
};
</script>

<style>
.home {
  background-color: rgb(33 31 31);
}
.movies {
  padding: 32px 16px;
}
.movie {
  position: relative;
  display: flex;
  flex-direction: column;
}
.movie-img {
  position: relative;
  overflow: hidden;

}
.movie-img img {
  display: block;
  width: 100%;
  height: 100%;
}
.review {
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 40px;
  height: 40px;
  background-color: #c92502;
  color: #fff;
  border-radius: 0 0 16px 0;
  box-shadow: 0 4px 6px -1px rgb(0 0 0 / 10%);
}
.overview {
  line-height: 1.5;
  position: absolute;
  bottom: 0;
  background-color: rgba(201, 38, 2, 0.9);
  padding: 12px;
  color: #fff;
  transform: translateY(100%);
  transition: all 0.5s ease-in-out;
  display: block;
}
.info {
  margin-top: auto;
}
.title {
  margin-top: 8px;
  color: #fff;
  font-size: 20px;
}
.release {
  margin-top: 8px;
  color: #c9c9c9;
}
.movie-img:hover .overview {
  transform: translateY(0);
  transition: all 0.5s ease-in-out;
}
.button-light {
  background-color: transparent;
  border: 1px solid #c92502;
  margin-top: 8px;
  font-size: 15px;
}
.movie-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  column-gap: 32px;

  row-gap: 64px;
}
@media (min-width: 1400px) {
  .container {
    max-width: 70%;
  }
}
@media (max-width: 1060px) {
  .movie-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    column-gap: 32px;

    row-gap: 64px;
  }
}
@media (max-width: 766px) {
  .movie-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    column-gap: 32px;

    row-gap: 64px;
  }
}
.search {
  display: flex;
  padding: 32px 16px;
}
.search-input {
  max-width: 350px;
  width: 100%;
  padding: 12px 6px;
  font-size: 14px;
  border: none;
  outline: none;
}
</style>
