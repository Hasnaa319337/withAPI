<template>
  <section class="hero">
    <img class="hero-img" src="../assets/images/movieHero.jpg" />
    <div class="text-container">
      <div class="text">
        <p class="paragraph">NOW STREAMING</p>
        <h1 class="main-heading">
          <span class="span-heading">Now</span> Streaming
        </h1>
        <nuxt-link class="button btn1" to="/">View Movies</nuxt-link>
        

      </div>
    </div>
  </section>
</template>

<script>

export default {

};
</script>

<style>
.hero {
  height: 500px;
  position: relative;
}
.hero:after {
  content: " ";
  position: absolute;
  top: 0;
  left: 0;
  background-color: rgba(0, 0, 0, 0.6);
  width: 100%;
  height: 100%;
}
.hero-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.text-container {
  z-index: 99;
  position: absolute;
  top: 0;
  margin: 0;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.text {
  padding: 0 16px;
  width: 100%;
  max-width: 1400px;
  margin: 0 auto;
}
.paragraph {
  font-weight: 600;
  font-size: 18px;
  text-transform: uppercase;
  color: #c92502;
  margin-bottom: 8px;
}
.span-heading {
  font-weight: bold;
}
.main-heading {
  color: #fff;
  font-size: 64px;
  font-weight: 200;
  margin-bottom: 15px;
}
.btn1{
 
  font-size: 20px;
  align-self: flex-start;

}
</style>
