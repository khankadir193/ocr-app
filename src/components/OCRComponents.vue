<template>
    <div>
      <input type="file" @change="handleUploadFile" />
      <img :src="imgUrl" alt="Uploaded Image" />
      <div>{{ recognizedText }}</div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'OCRComponents',
    data() {
      return {
        imgUrl: '',
        recognizedText: '',
      };
    },
    methods: {
      handleUploadFile(event) {
        const file = event.target.files[0];
        if (file) {
          const reader = new FileReader();
          reader.onload = (e) => {
            this.imgUrl = e.target.result;
            this.IntegrationOCR(file);
          };
          reader.readAsDataURL(file);
        }
      },
      async IntegrationOCR(file) {
        const formData = new FormData();
        formData.append('image', file);
  
        // Use axios or fetch to send the image data to the server
        // Replace the placeholder URL with your actual server endpoint
        const serverEndPoint = 'http://localhost:3000/perform-ocr';
        await fetch(serverEndPoint, {
          method: 'POST',
          body: formData,
        })
          .then((response) => response.json())
          .then((data) => {
            console.log('Recognized Text:', data.text);
            this.recognizedText = data.text;
          })
          .catch((error) => {
            console.error('Error during fetch:', error);
        });

      },
    },
  };
  </script>
  
  <style scoped></style>
  