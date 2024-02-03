<template>
  <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  <!-- <OCRComponents /> -->
  <!-- <FIleUploadOCR /> -->
  <FileUpload2 />
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
// import OCRComponents from './components/OCRComponents.vue';
// import FIleUploadOCR from './components/FIleUploadOCR.vue';
import FileUpload2 from './components/FileUpload2.vue';
export default {
  name: 'App',
  components: {
    // HelloWorld,
    // OCRComponents
    // FIleUploadOCR
    FileUpload2
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
