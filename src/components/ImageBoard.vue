<template>
  <div class="image-board">
    <ImageCard v-for="(image, index) in images" :key="index" :image="image" @click="swapImages(index)" />
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
      images: []
    };
  },
  mounted() {
    this.images = this.generateImages();
  },
  methods: {
    generateImages() {
      const list = Array.from({ length: 15 }, (_, index) => index + 1);
      return list.map((path, index) => ({
        id: index,
        src: `/src/assets/images/${path}.jpg`,
        alt: `Image ${index + 1}`,
        width: '100px',
        height: '100px',
        left: `${Math.floor(Math.random() * (window.innerWidth - 100))}px`,
        top: `${Math.floor(Math.random() * (window.innerHeight - 100))}px`
      }));
    },
    getRandomIndex(currentIndex, length) {
      let randomIndex = Math.floor(Math.random() * length);
      while (randomIndex === currentIndex) {
        randomIndex = Math.floor(Math.random() * length);
      }
      return randomIndex;
    },
    swapImages(index) {
      const targetIndex = this.getRandomIndex(index, this.images.length);
      const tempTop = this.images[index].top;
      const tempLeft = this.images[index].left;

      this.images[index].top = this.images[targetIndex].top;
      this.images[index].left = this.images[targetIndex].left;

      this.images[targetIndex].top = tempTop;
      this.images[targetIndex].left = tempLeft;
    }
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