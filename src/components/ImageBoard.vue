<template>
  <div class="image-board">
    <ImageCard v-for="(image, index) in images" :key="index" :image="image" @click="moveImage(index, $event)" :class="{ 'image-move': image.move }" />
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
        top: `${Math.floor(Math.random() * (window.innerHeight - 100))}px`,
        move: false // 添加一个属性来控制是否添加.image-move类
      }));
    },
    moveImage(index, event) {
      this.images[index].top = `${parseInt(this.images[index].top) - 100}px`;
      this.images[index].move = true; // 点击后设置move为true
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

.image-move {
  transition: all 0.618s ease;
}
</style>