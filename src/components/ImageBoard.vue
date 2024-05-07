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
      images: []
    };
  },
  created() {
    const list = this.getDigits(10);

    this.images = list.map((path, index) => ({
      src: `/src/assets/images/${path}.jpg`,
      alt: `Image ${index + 1}`,
      width: '100px',
      height: '100px',
      left: `${Math.floor(Math.random() * (window.innerWidth - 100))}px`,
      top: `${Math.floor(Math.random() * (window.innerHeight - 100))}px`
    }));
  },
  methods: {
    getDigits: (n) => {
      return Array.from({ length: n }, (_, index) => index + 1);
    }
  }
};
</script>

<!-- <script>
import ImageCard from './ImageCard.vue';

export default {
  name: 'ImageBoard',
  components: {
    ImageCard
  },
  computed: {
    images() {
      const list = this.getDigits(10);

      return list.map((path, index) => ({
        src: `/src/assets/images/${path}.jpg`,
        alt: `Image ${index + 1}`,
        width: '100px',
        height: '100px',
        left: `${Math.floor(Math.random() * (window.innerWidth - 100))}px`,
        top: `${Math.floor(Math.random() * (window.innerHeight - 100))}px`
      }));
    }
  },
  methods: {
    getDigits: (n) => {
      return Array.from({ length: n }, (_, index) => index + 1);
    }
  }
};
</script> -->

<style scoped>
.image-board {
  display: flex;
  width: 100%;
  height: 100%;
  justify-content: center;
  align-items: center;
}
</style>