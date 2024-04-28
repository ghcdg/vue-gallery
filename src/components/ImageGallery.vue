<template>
  <div class="image-gallery">
    <div class="image-board-container">
      <!-- <ImageBoard>
        <ImageCard src="/src/assets/images/1.jpg" width="161.8px" height="161.8px" alt="示例图片" />
      </ImageBoard> -->

      <ImageBoard :images="imagesArray" :left="left" :middle="middle" :right="right">
      </ImageBoard>


    </div>
  </div>
</template>

<script>
import ImageBoard from './ImageBoard.vue';
import ImageCard from './ImageCard.vue';


export default {
  components: {
    ImageBoard,
    ImageCard
  },

  data() {
    return {
      imagesArray: [
        { src: '/src/assets/images/1.jpg', alt: '示例图片1', width: '100px', height: '100px' },
        { src: '/src/assets/images/1.jpg', alt: '示例图片2', width: '100px', height: '100px' },
        { src: '/src/assets/images/1.jpg', alt: '示例图片3', width: '100px', height: '100px' },
        // Add more images as needed
      ],
      left: { 
        width: "400px", 
        height: "400px" 
      },
      middle: { 
        width: "400px", 
        height: "400px" 
      },
      right: { 
        width: "400px", 
        height: "400px" 
      }
    };
  }
}
</script>

<style scoped>
.image-gallery {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
  /* vh 单位代表视窗（看到的浏览器窗口）的大小高度的百分比 */
  /* height: 100vh;   */
}

.image-board-container {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>