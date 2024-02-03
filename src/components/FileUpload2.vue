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
    name: 'FileUpload2',
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
            const apikey = 'helloworld'; // Replace with your OCR API key
            const language = 'eng'; // Adjust the language code as needed
            const url = "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRiz2JE_h1wmLG1hcXyF-4IMsItOC4vDlZ0_yW4DUBtdw&s";

            const frmData = new FormData();
            frmData.append('apikey', apikey);
            frmData.append('language', language);
            frmData.append('url', url);

            const headers = {
                'Content-Type': 'multipart/form-data', // Important for sending form data
                // Add other headers as needed
            };

            if (this.imageUrl) {
                // Make a POST request to the OCR API
                axios.post('https://api.ocr.space/parse/image',frmData,{headers})
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
  