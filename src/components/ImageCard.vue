<template>
    <div class="image-card" @click="toggleFlip">
      <img :src="src" :alt="alt" :style="{ width: width, height: height }" :class="{ 'flipped': isFlipped }" />
    </div>
  </template>
  
  <script>
  export default {
    name: 'ImageCard',
    props: {
      src: {
        type: String,
        required: true
      },
      alt: {
        type: String,
        default: ''
      },
      width: {
        type: String,
        default: 'auto'
      },
      height: {
        type: String,
        default: 'auto'
      }
    },
    data() {
      return {
        isFlipped: false
      };
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
    /* perspective: 1000px;
    cursor: pointer; */
    display: inline-block;
    border-radius: 4px;
    overflow: hidden;
    
    transition: transform 0.618s ease;
  }

  .image-card:hover {
    box-shadow: 0px 3px 6px rgba(230, 5, 5, 0.349);
    transform: translateY(-16.18px) scale(1.068);

    transition: transform 0.618s ease;

  }
  
  .image-card img {
    display: block;
    object-fit: cover;
    /* transform-style: preserve-3d; */
    /* backface-visibility: hidden; */

    transition: transform 0.618s;
  }
  
  .image-card img.flipped {
    transform: rotateY(180deg);
  }
  </style>
  