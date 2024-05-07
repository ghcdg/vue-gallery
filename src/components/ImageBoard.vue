<template>
  <div class="image-board">
    <ImageCard v-for="(image, index) in images" :key="index" :image="image" />
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
      images: [
        { src: '/src/assets/images/1.jpg', alt: '示例图片1', width: '100px', height: '100px', left: '10px', top: '100px' },
        { src: '/src/assets/images/2.jpg', alt: '示例图片2', width: '100px', height: '100px', left: '10px', top: '100px' },
        { src: '/src/assets/images/3.jpg', alt: '示例图片3', width: '100px', height: '100px', left: '10px', top: '100px' },
        { src: '/src/assets/images/4.jpg', alt: '示例图片4', width: '100px', height: '100px', left: '10px', top: '100px' },
        { src: '/src/assets/images/5.jpg', alt: '示例图片5', width: '100px', height: '100px', left: '10px', top: '100px' }
      ]
    };
  },
  mounted() {
    this.images.forEach(image => {
      const randomLeft = Math.floor(Math.random() * (window.innerWidth - 100)); // Random left position within window width
      const randomTop = Math.floor(Math.random() * (window.innerHeight - 100)); // Random top position within window height
      image.left = `${randomLeft}px`;
      image.top = `${randomTop}px`;
    });
  }
};
</script>

<style scoped>
.image-board {
  display: flex;
  width: 100%;
  height: 100%;
  justify-content: center;
  align-items: center;
}
</style>