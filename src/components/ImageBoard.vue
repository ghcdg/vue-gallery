<template>
  <div class="image-board">

      <ImageCard v-for="(image, index) in leftImages" :key="index" :image="image" @click="swapImages(image.id)" :style="{ top: image.top, left: image.left }" />
      <ImageCard v-if="middleImage" :image="middleImage" @click="swapImages(middleImage.id)" :style="{ top: middleImage.top, left: middleImage.left }" />
      <ImageCard v-for="(image, index) in rightImages" :key="index" :image="image" @click="swapImages(image.id)" :style="{ top: image.top, left: image.left }" />
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
      leftImages: [],
      middleImage: null,
      rightImages: [],
      defaultWidth: 100,
      defaultHeight: 100,
      leftAreaWidth: window.innerWidth * 0.4,
      centerAreaWidth: window.innerWidth * 0.2,
      rightAreaWidth: window.innerWidth * 0.4
    };
  },
  mounted() {
    this.images = this.generateImages();
    this.leftImages = this.images.filter(image => image.area === 'left');
    this.middleImage = this.images.find(image => image.area === 'middle');
    this.rightImages = this.images.filter(image => image.area === 'right');
  },
  methods: {
    generateImages() {
      const list = Array.from({ length: 15 }, (_, index) => index + 1);
      return list.map((path, index) => {
        let area;
        if (index === 0) {
          area = 'middle';
        } else {
          area = index % 2 === 0 ? 'left' : 'right';
        }
        let left;
        if (area === 'left') {
          left = `${Math.floor(Math.random() * (this.leftAreaWidth - this.defaultWidth))}px`;
        } else if (area === 'right') {
          left = `${this.leftAreaWidth + this.centerAreaWidth + Math.floor(Math.random() * (this.rightAreaWidth - this.defaultWidth))}px`;
        } else {
          left = `${(window.innerWidth - this.defaultWidth) / 2}px`;
        }
        return {
          id: index,
          src: `/src/assets/images/${path}.jpg`,
          alt: `Image ${index + 1}`,
          width: `${this.defaultWidth}px`,
          height: `${this.defaultHeight}px`,
          left: left,
          top: `${Math.floor(Math.random() * (window.innerHeight - this.defaultHeight))}px`,
          area: area
        };
      });
    },
    swapImages(imageId) {
      const imageIndex = this.images.findIndex(image => image.id === imageId);
      const targetIndex = this.getRandomIndex(imageIndex, this.images.length);
      const tempTop = this.images[imageIndex].top;
      const tempLeft = this.images[imageIndex].left;

      this.images[imageIndex].top = this.images[targetIndex].top;
      this.images[imageIndex].left = this.images[targetIndex].left;

      this.images[targetIndex].top = tempTop;
      this.images[targetIndex].left = tempLeft;

      this.leftImages = this.images.filter(image => image.area === 'left');
      this.middleImage = this.images.find(image => image.area === 'middle');
      this.rightImages = this.images.filter(image => image.area === 'right');
    },
    getRandomIndex(currentIndex, length) {
      let randomIndex = Math.floor(Math.random() * length);
      while (randomIndex === currentIndex) {
        randomIndex = Math.floor(Math.random() * length);
      }
      return randomIndex;
    }
  }
};
</script>

<style scoped>
.image-board {
  display: flex;
  height: 100%;
}
</style>