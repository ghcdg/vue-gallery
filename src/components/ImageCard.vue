<template>
    <div class="image-card">
      <img :src="src" :alt="alt" :style="{ width: size, height: size }" />
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
      size: {
        type: String,
        default: '150px'
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
    transition: transform 0.3s ease;
  }
  
  .image-card:hover {
    transform: translateY(-5px);
  }
  
  .image-card img {
    display: block;
    object-fit: cover;
  }
  </style>
  