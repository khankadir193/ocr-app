<template>
  <div>
    <h1>VueDropDown</h1>
    <vue-dropzone ref="myVueDropzone" id="dropzone" :options="dropzoneOptions"></vue-dropzone>

  </div>
</template>

<script>

import vue2Dropzone from 'vue2-dropzone'
import 'vue2-dropzone/dist/vue2Dropzone.min.css'
export default {
  name: 'app',
  components: {
    vueDropzone: vue2Dropzone
  },
  data: function () {
    return {
      dropzoneOptions: {
          url: 'https://httpbin.org/post',
          thumbnailWidth: 150,
          maxFilesize: 0.5,
          headers: { "My-Awesome-Header": "header value" }
      }
    }
  }
,
  methods: {
    onFileUploadSuccess(file) {
      // Access file information
      console.log('Uploaded File:', file);

      // Access relative path (example: "uploads/myfile.jpg")
      const relativePath = file.relativePath;
      console.log('Relative Path:', relativePath);
    },
  },
};
</script>
