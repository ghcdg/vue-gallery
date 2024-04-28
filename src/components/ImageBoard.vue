<template>
  <div class="image-board">
    <div class="left" :style="{ width: left.width, height: left.height }">
    </div>
    <div class="middle" :style="{ width: middle.width, height: middle.height }">
      <!-- <slot></slot> -->
    </div>
    <div class="right" :style="{ width: right.width, height: right.height }">
      <div v-for="(image, index) in images" :key="index">
        <ImageCard :src="image.src" :alt="image.alt" :width="image.width" :height="image.height" />
      </div>
    </div>
  </div>
</template>

<script>
import ImageCard from './ImageCard.vue';

export default {
  name: 'ImageBoard',
  components: {
    ImageCard
  },
  props: {
    left: {
      type: Object,
      // default: {
      //   width: 'auto',
      //   height: 'auto'
      // }
    },
    right: {
      type: Object,
      // default: {
      //   width: 'auto',
      //   height: 'auto'
      // }
    },
    middle: {
      type: Object,
      // default: {
      //   width: 'auto',
      //   height: 'auto'
      // }
    },
    images: {
      type: Array,
      required: true
    }
  }
}
</script>

<style scoped>
.image-board {
  display: flex;
  width: 100%;
  height: 100%;
  justify-content: center;
  align-items: center;
}

.left,
.right {
  flex: 4;
  /* Each will take up 40% of the space */
}

.middle {
  flex: 2;
  /* Middle will take up 20% of the space */
  display: flex;
  justify-content: center;
  align-items: center;
}

.image-card-wrapper {
  width: 100%;
  /* Full width of the middle section */
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
