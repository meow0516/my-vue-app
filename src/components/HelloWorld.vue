<template>
  <div  class="outer">
    <Carousel class="inner">
      <Slide class="slide" v-for="slide in mockSlides" :key="slide">
        <div class="carousel__item">
          <img :src="getImage(slide.img)" alt="">
        </div>
      </Slide>
  
      <template #addons>
        <Navigation />
        <Pagination />
      </template>
    </Carousel>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
.outer {
  width: 50%;
  /* height: auto; */
  /* background-position: center; */
  background-size: contain;
  background-repeat: no-repeat;
  background-image: url('../assets/img-step-screen-phone.aa3c7e0c.png');
}

.inner {
  width: 95%;
  margin: 0 auto;
}

.inner :deep(.carousel__viewport) {
  border-radius: 10em;
}
.carousel__item {
  width: 100%;
}

img {
  width: 100%;
}
</style>

<script setup>
import { ref } from 'vue'
import 'vue3-carousel/dist/carousel.css'
import { Carousel, Slide, Pagination, Navigation } from 'vue3-carousel'

const mockSlides = ref([{
  id:1,
  img: '../assets/img-step-screen-1-1.png'
},
{
  id:2,
  img: '../assets/img-step-screen-1-2.png'
},
{
  id:3,
  img: '../assets/img-step-screen-1-3.png'
},
{
  id:4,
  img: '../assets/img-step-screen-2-1.png'
},
{
  id:5,
  img: '../assets/img-step-screen-2-2.png'
},
{
  id:6,
  img: '../assets/img-step-screen-2-3.png'
},
])

const getImage=(img)=> {
  return new URL(img, import.meta.url).href
  }

const count = ref(0)
</script>