<template>
    <div>
      <input type="file" @change="handleUploadFile">
      <button @click="submitImage">Submit</button>
    </div>
  </template>
  
  <script>
  export default {
    name:"FileUploadOCR",
    data() {
      return {
        selectedFile: null
      };
    },
    methods: {
      handleUploadFile(event) {
        this.selectedFile = event.target.files[0];
      },
      async submitImage() {
        try {
          const formData = new FormData();
          formData.append('image', this.selectedFile);
            
          const serverEndPoint = 'http://localhost:4000/upload';
  
          const response = await fetch(serverEndPoint, {
            method: 'POST',
            body: formData
          });
  
          const result = await response.json();
          console.log('result...????????',result);
        } catch (error) {
          console.error('Error uploading image:', error);
        }
      }
    }
  };
  </script>
  