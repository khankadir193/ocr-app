<template>
  <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  <!-- <OCRComponents /> -->
  <FIleUploadOCR />
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
// import OCRComponents from './components/OCRComponents.vue';
import FIleUploadOCR from './components/FIleUploadOCR.vue';
export default {
  name: 'App',
  components: {
    // HelloWorld,
    // OCRComponents
    FIleUploadOCR
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
