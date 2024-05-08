<template>
  <div class="image-card" :style="{ left: image.left, top: image.top }" @click="toggleFlip">
    <img :src="image.src" :alt="image.alt" :style="{ width: image.width, height: image.height }" :class="{ 'flipped': isFlipped }" />
  </div>
</template>

<script>
export default {
  name: 'ImageCard',
  props: {
    image: {
      type: Object,
      required: true,
      default: () => ({
        src: '',
        alt: '',
        width: 'auto',
        height: 'auto',
        left: '10px',
        top: '10px'
      })
    }
  },
  data() {
    return {
      isFlipped: false
    };
  },
  mounted() {
    // No need to assign left and top here, as they are bound directly to props
  },
  methods: {
    toggleFlip() {
      this.isFlipped = !this.isFlipped;
    }
  }
}
</script>

<style scoped>
.image-card {
  position: absolute;
  display: inline-block;
  border-radius: 4px;
  overflow: hidden;
  transition: all 0.618s ease;
}

.image-card:hover {
  box-shadow: 0px 3px 6px rgba(230, 5, 5, 0.349);
  transform: translateY(-16.18px) scale(1.068);
}
  
.image-card img {
  display: block;
  object-fit: cover;
}

.image-card img.flipped {
  transform: rotateY(180deg);
}
</style>