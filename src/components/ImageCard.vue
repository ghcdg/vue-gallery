<template>
  <div class="image-card" :style="cardStyle" @click="handleClick">
    <img :src="image.src" :alt="image.alt" :style="imageStyle" :class="{ 'flipped': isFlipped }" />
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
        left: '0px',
        top: '0px',
        toFlipMe: true,        
      })
    }
  },
  data() {
    return {
      isFlipped: false
    };
  },
  computed: {
    cardStyle() {
      return {
        left: this.image.left,
        top: this.image.top
      };
    },
    imageStyle() {
      return {
        width: this.image.width,
        height: this.image.height
      };
    }
  },
  mounted() {
    // console.log(this.image)
  },
  methods: {
    handleClick() {
      // if current image has flag "toFlipMe", use the flag
      // if current image has no flag "toFlipMe", flip the image by default
      this.isFlipped = (this.image.toFlipMe === false) ? this.isFlipped : !this.isFlipped;
    },
  }
};
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
  transition: all 0.618s ease;
}

.image-card img {
  transform: rotateY(0deg);
  transition: all 0.618s ease;
}
</style>