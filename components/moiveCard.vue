<template>
  <div class="movie">
    <div class="movie-img">
      <img :src="imgSrc(data.movieImg)" />
      <div class="review">{{ data.review }}</div>
      <div class="overview">{{ data.overview }}</div>
    </div>

    <div class="info">
      <title class="title">{{ data.title }}</title>
      <p class="release">Released:{{ data.release }}</p>
      <nuxt-link
        class="button button-light"
        :to="{ name: 'movies-movieid', params: { movieid: data.id } }"
        >Get More Info</nuxt-link
      >
    </div>
  </div>
</template>

<script>

export default {
  props: ["data"],

  methods: {
    imgSrc(image) {
      return require(`@/assets/images/${image}`);
    },
  },
};
</script>

<style>
.movie {
  position: relative;
  display: flex;
  flex-direction: column;
}
.movie-img {
  position: relative;
 
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
  box-shadow: 0 4px 6px -1px rgb(0 0 0 / 10%), 0 2px 4px -1px rgb(0 0 0 / 6%);
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
</style>
