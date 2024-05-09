<template>
  <div class="image-board">
    <ImageCard v-for="(image, index) in images" :key="index" :image="image" @click="swapImages(index)" :style="{ top: image.top, left: image.left }" />
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
      images: [],
      defaultWidth: 100,
      defaultHeight: 100,
    };
  },
  mounted() {
    this.images = this.generateImages();
      // 将第一张图片放在界面的正中间
      this.images[0].top = `${(window.innerHeight - this.defaultHeight) / 2}px`;
      this.images[0].left = `${(window.innerWidth - this.defaultWidth) / 2}px`;
  },
  methods: {
    generateImages() {
      const list = Array.from({ length: 15 }, (_, index) => index + 1);
      return list.map((path, index) => ({
        id: index,
        src: `/src/assets/images/${path}.jpg`,
        alt: `Image ${index + 1}`,
        width: `${this.defaultWidth}px`,
        height: `${this.defaultHeight}px`,
        left: `${Math.floor(Math.random() * (window.innerWidth - this.defaultWidth))}px`,
        top: `${Math.floor(Math.random() * (window.innerHeight - this.defaultHeight))}px`
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
  position: relative;
  width: 100%;
  height: 100%;
}
</style>