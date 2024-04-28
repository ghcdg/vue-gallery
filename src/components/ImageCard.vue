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
    
    transition: transform 0.68s ease;
  }

  .image-card:hover {
    box-shadow: 0px 3px 6px rgba(248, 247, 247, 0.986);
    transform: translateY(-15px);

    transition: transform 0.68s ease;

  }
  
  .image-card img {
    display: block;
    object-fit: contain;
    transform-style: preserve-3d;
    /* backface-visibility: hidden; */

    transition: transform 0.68s;
  }
  
  .image-card img.flipped {
    transform: rotateY(180deg);
  }
  </style>
  