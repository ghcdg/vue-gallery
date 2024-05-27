<template>
  <div class="image-board">
    <ImageCard
      v-for="(image, index) in images"
      :key="image.id"
      :image="image"
      :style="{ width: defaultWidth + 'px', height: defaultHeight + 'px' }"
      @click="swapImages(image.id)"
    />
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
      middleImageID: 0,
      windowWidth: window.innerWidth,
      leftAreaWidth: 40,  // Use percentage
      centerAreaWidth: 20, // Use percentage
      rightAreaWidth: 40  // Use percentage
    };
  },
  computed: {
    defaultWidth() {
      return this.windowWidth * 0.078;
    },
    defaultHeight() {
      return this.windowWidth * 0.078;
    }
  },
  mounted() {
    this.initializeImages();
    window.addEventListener('resize', this.handleResize);
  },
  beforeUnmount() {
    window.removeEventListener('resize', this.handleResize);
  },
  methods: {
    handleResize() {
      this.windowWidth = window.innerWidth;
      // this.initializeImages();
      this.images = this.images.map(image => ({
        ...image,
        width: `${this.defaultWidth}px`,
        height: `${this.defaultHeight}px`
      }));
    },
    initializeImages() {
      this.images = this.shuffleArray(this.generateImages());

      const half = Math.ceil(this.images.length / 2);

      const middleImage = this.generateMiddleImage(this.images[0]);
      const leftImages = this.generateLeftAreaImages(this.images.slice(1, half));
      const rightImages = this.generateRightAreaImages(this.images.slice(half));

      this.middleImageID = middleImage.id;
      this.images = leftImages.concat(middleImage, rightImages);
    },
    generateImages() {
      return Array.from({ length: 15 }, (_, index) => ({
        id: index,
        src: `/src/assets/images/${index + 1}.jpg`,
        alt: `Image ${index + 1}`,
        width: `${this.defaultWidth}px`,
        height: `${this.defaultHeight}px`,
        left: '0%',
        top: '0%'
      }));
    },
    swapImages(selectedID) {
      if (selectedID === this.middleImageID) return;

      const selectedImage = this.images.find(image => image.id === selectedID);
      const middleImage = this.images.find(image => image.id === this.middleImageID);

      [selectedImage.left, middleImage.left] = [middleImage.left, selectedImage.left];
      [selectedImage.top, middleImage.top] = [middleImage.top, selectedImage.top];

      this.middleImageID = selectedImage.id;
    },
    generateMiddleImage(image) {
      return {
        ...image,
        left: '50%',
        top: '50%',
        transform: 'translate(-50%, -50%)'
      };
    },
    generateLeftAreaImages(images) {
      return images.map(image => ({
        ...image,
        left: `${Math.random() * (this.leftAreaWidth - (this.defaultWidth / this.windowWidth * 100))}%`,
        top: `${Math.random() * (100 - (this.defaultHeight / window.innerHeight * 100))}%`
      }));
    },
    generateRightAreaImages(images) {
      return images.map(image => ({
        ...image,
        left: `${this.leftAreaWidth + this.centerAreaWidth + Math.random() * (this.rightAreaWidth - (this.defaultWidth / this.windowWidth * 100))}%`,
        top: `${Math.random() * (100 - (this.defaultHeight / window.innerHeight * 100))}%`
      }));
    },
    shuffleArray(arr) {
      const newArr = arr.slice();
      for (let i = newArr.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [newArr[i], newArr[j]] = [newArr[j], newArr[i]];
      }
      return newArr;
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