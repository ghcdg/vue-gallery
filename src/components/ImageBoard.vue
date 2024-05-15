<template>
  <div class="image-board">
    <ImageCard v-for="(image, index) in images" :key="index" :image="image" @click="swapImages(image.id)" :style="{ top: image.top, left: image.left }" />
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
      middleImageID: 0,
      rightImages: [],
      defaultWidth: 100,
      defaultHeight: 100,
      leftAreaWidth: window.innerWidth * 0.4,
      centerAreaWidth: window.innerWidth * 0.2,
      rightAreaWidth: window.innerWidth * 0.4,

    };
  },
  mounted() {

    this.images = this.generateImages();
    this.images = this.shuffleArray(this.images);
    var len = this.images.length;
    var half = Math.ceil(len/2);

    this.middleImage = this.generateMiddleImage(this.images[0]);
    this.leftImages = this.generateLeftAreaImages(this.images.slice(1, half));
    this.rightImages = this.generateRightAreaImages(this.images.slice(half, len));

    this.middleImageID = this.middleImage.id;
    this.images = this.leftImages.concat(this.middleImage).concat(this.rightImages);

  },
  methods: {
    generateImages() {
      const list = Array.from({ length: 15 }, (_, index) => index + 1);
      return list.map((path, index) => {        
        return {
          id: index,
          src: `/src/assets/images/${path}.jpg`,
          alt: `Image ${index + 1}`,
          width: `${this.defaultWidth}px`,
          height: `${this.defaultHeight}px`,
          left: `0px`,
          top: `0px`
        };
      });
    },

    swapImages(selectedID) {

      const selectedImage = this.images.find(image => image.id === selectedID);
      if (selectedID === this.middleImageID) return;
      
      const targetImage = this.images.find(image => image.id === this.middleImageID);

      const tempTop = selectedImage.top;
      const tempLeft = selectedImage.left;

      selectedImage.top = targetImage.top;
      selectedImage.left = targetImage.left;

      targetImage.top = tempTop;
      targetImage.left = tempLeft;

      this.middleImageID = selectedImage.id;
    },

    getRandomImage(images) {
      return this.shuffleArray(images)[0];
    },

    generateMiddleImage(image) {
      const left = `${(window.innerWidth - this.defaultWidth) / 2}px`;
      const top = `${(window.innerHeight - this.defaultHeight) / 2}px`;
      return {...image, left, top};
    },

    generateLeftAreaImages(images) {
      return images.map(image => {
        const left = `${Math.floor(Math.random() * (this.leftAreaWidth - this.defaultWidth))}px`;
        const top = `${Math.floor(Math.random() * (window.innerHeight - this.defaultHeight))}px`;
        return {...image, left, top};
      });
    },

    generateRightAreaImages(images) {
      return images.map(image => {
        const left = `${this.leftAreaWidth + this.centerAreaWidth + Math.floor(Math.random() * (this.rightAreaWidth - this.defaultWidth))}px`;
        const top = `${Math.floor(Math.random() * (window.innerHeight - this.defaultHeight))}px`;
        return {...image, left, top};
      });
    },     
    
    /**
     * shuffle array data
     * @param {array} arr input array
     * @returns {array}
     */
    shuffleArray(arr) {
      // Create a new array to avoid mutating the original array
      let newArr = arr.slice();

      // Shuffle the new array using Fisher-Yates algorithm
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
  display: flex;
  height: 100%;
}
</style>