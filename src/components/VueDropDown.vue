<template>
  <div>
    <h1>VueDropDown</h1>
    <vue2-dropzone
      id="my-dropzone"
      ref="myDropzone"
      :options="dropzoneOptions"
      @vdropzone-success="onFileUploadSuccess"
    ></vue2-dropzone>
  </div>
</template>

<script>
// import 'vue2-dropzone/dist/vue2Dropzone.min.css'; // Import the CSS for styling
// import VueDropzone from 'vue2-dropzone'; // Import the VueDropzone component
// import 'dropzone/dist/dropzone.min.css'; // Import Dropzone.js styles

export default {
  name: 'VueDropDown',
  components: {
    // VueDropzone,
  },
  data() {
    return {
      dropzoneOptions: {
        url: '/your-upload-endpoint', // Set your upload endpoint
        // Other Dropzone.js options...
      },
    };
  },
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
