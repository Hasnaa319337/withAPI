<template>
  <!-- Movie Info -->
  <div class="app">
  <div class="single-movie container">
    <NuxtLink class="button" :to="{ name: 'index' }"> Back </NuxtLink>
    <div class="movie-info">
      <div class="movie-img">
        <img :src="`https://image.tmdb.org/t/p/w500/${item.poster_path}`" alt="" />
      </div>
      <div class="movie-content">
        <h1>Title: {{ item.title }}</h1>
        <p class="movie-fact tagline">
          <span>Tagline:</span> "{{ item.tagline }}"
        </p>
        <p class="movie-fact">
          <span>Released:</span>
          {{
            new Date(item.release_date).toLocaleString("en-us", {
              month: "long",
              day: "numeric",
              year: "numeric",
            })
          }}
        </p>
        <p class="movie-fact">
          <span>Duration:</span> {{ item.runtime }} minutes
        </p>
        <p class="movie-fact">
          <span>Revenue:</span>
          {{
            new Date(item.revenue).toLocaleString("en-us", {
              style: "currency",
              currency: "USD",
            })
          }}
        </p>
        <p class="movie-fact"><span>Overview:</span> {{ item.overview }}</p>
      </div>
    </div>
  </div>
</div>
</template>

<script>


export default {
  async asyncData({$axios, $route,params }) {
    const data = await $axios.$get(
      `https://api.themoviedb.org/3/movie/${$route.params.id}?api_key=37ed43a4f8eaa2abd75f9283692947bc&language=en-US`
    );
    console.log(data);
    // return {
    //   item: data,
    // };
  },

  data() {
    return {
      item: "",
    };
  },
  methods: {},
};
</script>

<style>
.single-movie {
  color: #fff;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 32px 16px;
}
.app{
  background-color: #211f1f;
    min-height: 100vh;
}
.button {
  align-self: flex-start;
  margin-bottom: 32px;
}

.movie-info {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 32px;
  color: #fff;

}
@media (min-width: 800px) {
   .movie-info{
    flex-direction: row;
    align-items: flex-start;
   }
  }
.movie-img img {
  max-height: 500px;
  width: 100%;
}

@media (min-width: 800px) {
  .movie-img {
    max-height: 700px;
    width: initial;
  }
}

.movie-content h1 {
  font-size: 56px;
  font-weight: 400;
}

.movie-fact {
  margin-top: 12px;
  font-size: 20px;
  line-height: 1.5;
}

span {
  font-weight: 600;
  text-decoration: underline;
}

.tagline {
  font-style: italic;
}
.tagline span {
  font-style: normal;
}
</style>
