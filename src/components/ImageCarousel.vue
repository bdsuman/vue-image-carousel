<script setup>
  import {ref, onMounted, onUnmounted} from 'vue'

  const activeIndex = ref(0)

  const carouselItems = [
    {
      image: 'https://images.unsplash.com/photo-1620765971982-c5c4e1d1bd75?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1100&q=80',
      title: 'First Slide Label',
      caption: 'Nulla vitae elit libero, a pharetra augue mollis interdum. Nulla vitae elit libero, a pharetra augue'
    },
    {
      image: 'https://images.unsplash.com/photo-1620765970846-3274335578d6?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1400&q=80',
      title: 'Second Slide Label',
      caption: 'Nulla vitae elit libero, a pharetra augue mollis interdum.'
    }
  ]

  const imageFilter = '-webkit-filter: grayscale(100%);filter: grayscale(100%);'

  const incrementActiveIndex = () =>{
    if(activeIndex.value === carouselItems.length -1){
      activeIndex.value = 0
    }
    else{
      activeIndex.value++
    }
  }

  let timerId = null;

  const startSlideShow = function(){
    timerId = setInterval(incrementActiveIndex, 3000)
  }

  const stopSlideShow = function(){
    clearInterval(timerId)
  }
 
  onMounted(() => {
    startSlideShow()
  })

  onUnmounted(() =>{
    stopSlideShow()
  })
</script>

<template>
  <h4>Vue 3 Image Carousel</h4>
  <ol class="carousel-thumnails">
    <img  @click="activeIndex = index" height="50" :style="activeIndex !== index?imageFilter:''" style="cursor: pointer;" class="mx-1" v-for="(thumnail, index) in carouselItems" :key="index" :src="thumnail.image" alt="">
  </ol>
  <div @mouseover="stopSlideShow" @mouseleave="startSlideShow" id="carouselExampleCaptions" class="carousel">    
    <ol class="carousel-indicators">
      <li @click="activeIndex = index" v-for="(items, index) in carouselItems" :key="index" :class="index === activeIndex?'active':''"></li>
    </ol>
    
    <div class="carousel-inner">        
      <div class="carousel-item active">           
        <img height="500" :src="carouselItems[activeIndex].image" class="d-block w-100 img img-responsive" alt="...">
        <div class="carousel-caption d-none d-md-block">
          <h5>{{ carouselItems[activeIndex].title }}</h5>
          <p>{{ carouselItems[activeIndex].caption }}</p>
        </div>
      </div>  
    </div>    
    <a @click.prevent="0 === activeIndex ? activeIndex = (carouselItems.length) - 1 : activeIndex--" class="carousel-control-prev" href="#" role="button">
      <span class="carousel-control-prev-icon" aria-hidden="true"></span>
      <span class="sr-only">Previous</span>
    </a>
    <a @click.prevent="(carouselItems.length) - 1 === activeIndex ? activeIndex = 0 : activeIndex++" class="carousel-control-next" href="#" role="button">
      <span class="carousel-control-next-icon" aria-hidden="true"></span>
      <span class="sr-only">Next</span>
    </a>
  </div>
</template>

<style>
</style>
