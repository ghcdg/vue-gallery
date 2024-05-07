<template>
  <div class="image-board">
    <ImageCard :image="image" />    
  </div>
</template>

<script>
import ImageCard from './ImageCard.vue';

export default {
  name: 'ImageBoard',
  components: {
    ImageCard
  },
  data() {
    return {
      image: { src: '/src/assets/images/1.jpg', alt: '示例图片1', width: '100px', height: '100px', left: '10px', top: '100px' }
    }
  }
}
</script>

<style scoped>
.image-board {
  display: flex;
  width: 100%;
  height: 100%;
  justify-content: center;
  align-items: center;
}


.image-card-wrapper {
  width: 100%;
  /* Full width of the middle section */
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
