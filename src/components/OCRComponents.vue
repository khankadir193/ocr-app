<template>
    <div>
        <input type="file" @change="handleUploadFile" /> <br><br><br>
        <img :src="imgUrl" alt="Uploaded Image" /><br><br>

        <label>Second uploading image for testing....</label><br><br>
        <input type="file" @change="handleFileChange" /> <br><br>
        <img :src="selectedImage" alt="Uploaded Image" />

        <div>{{ recognizedText }}</div>
    </div>
</template>
  
<script>
import axios from 'axios';
export default {
    name: 'OCRComponents',
    data() {
        return {
            imgUrl: '',
            recognizedText: '',
            selectedImage:''
        };
    },
    methods: {
        handleUploadFile(event) {
            const file = event.target.files[0];
            console.log('file...????', file);
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
        async handleFileChange(event) {
            const file = event.target.files[0];

            if (file) {
                const reader = new FileReader();
                console.log('reader...???',reader);
                reader.onload = async(e) => {
                    console.log('onLoadEvent...eeee',e.target.result);
                    this.selectedImage = e.target.result;
                    const ocrApi = await `https://api.ocr.space/parse/imageurl?apikey=K89496159888957&url=${e.target.result}`;
                    const response = await axios.get(ocrApi);
                    console.log('ocrApi.....???????',response);
                };
                reader.readAsDataURL(file);
            }
        },
    },
};
</script>
  
<style scoped></style>
  


  <!-- https://api.ocr.space/parse/imageurl?apikey=helloworld&url=https://dl.a9t9.com/ocr/solarcell.jpg -->