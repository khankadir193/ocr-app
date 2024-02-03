<template>
    <div>
      <input type="file" @change="handleFileUpload">
      <img :src="imageUrl" alt="Uploaded Image">
  
      <!-- Add a button to trigger the OCR API request -->
      <button @click="submitToOCR">Submit to OCR</button>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    name:'FileUpload2',
    data() {
      return {
        imageUrl: null,
      };
    },
    methods: {
      handleFileUpload(event) {
        const fileInput = event.target;
        const file = fileInput.files[0];
  
        if (file) {
          this.convertImageToDataUrl(file);
        }
      },
      convertImageToDataUrl(file) {
        const reader = new FileReader();
  
        reader.onload = (e) => {
          this.imageUrl = e.target.result;
        };
  
        // Read the file as a data URL
        reader.readAsDataURL(file);
      },
      submitToOCR() {
        if (this.imageUrl) {
          // Make a POST request to the OCR API
          axios.post('https://api.ocr.space/parse/image', {
            apikey: 'YOUR_OCR_API_KEY', // Replace with your OCR API key
            language: 'eng', // Adjust the language code as needed
            base64image: this.imageUrl,
          })
          .then(response => {
            // Handle OCR API response
            const ocrResult = response.data;
            console.log('OCR Result:', ocrResult);
          })
          .catch(error => {
            console.error('Error making OCR API request:', error);
          });
        } else {
          console.error('No image to submit to OCR');
        }
      },
    },
  };
  </script>
  