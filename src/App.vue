<script setup>
import HelloWorld from './components/HelloWorld.vue'
import ImageGallery from './components/ImageGallery.vue';
import ImageBoard from './components/ImageBoard.vue';
import TheWelcome from './components/TheWelcome.vue'

</script>

<template>
  <header>
    <!-- <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div> -->

  </header>

  <main>
    <!-- <TheWelcome /> -->
    <div class="image-gallery-container">
      <ImageBoard />
    </div>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

.image-gallery-container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  /* height: 100%; */
  /* vh 单位代表视窗（看到的浏览器窗口）的大小高度的百分比 */
  height: 100vh;  
}

@media (min-width: 2048px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
