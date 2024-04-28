<template>
    <div class="image-card">
      <img :src="src" :alt="alt" :style="{ width: width, height: height }" />
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
    }
  }
  </script>
  
  <style scoped>
  .image-card {
    display: inline-block;
    border-radius: 4px;
    overflow: hidden;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    transition: transform 0.68s ease;
  }
  
  .image-card:hover {
    transform: translateY(-15px) scale(1.2) rotateY(180deg);
  }
  
  .image-card img {
    display: block;
    object-fit: cover;
  }
  </style>
  