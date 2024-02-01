<template>
    <div>
        <input type="file" @change="handleUploadFile" />
        <img :src="imgUrl" alt="Uploaded Image">
    </div>
</template>

<script>
// import axios from 'axios';
export default {
    name: 'OCRComponents',
    data() {
        return {
            imgUrl: 'https://images.pexels.com/photos/674010/pexels-photo-674010.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
            recognizedText: ''
        }
    },
    methods: {
        handleUploadFile(event) {
            console.log('event...???', event.target.files[0]);
            const file = event.target.files[0].name;
            if (file)
                console.log('file is true...')
            if (file) {
                const reader = new FileReader(file);
                console.log('reader...??', reader);
                this.IntegrationOCR();
                // reader.onload = (e) => {
                //     console.log('e.target.result', e.target.result);
                //     this.imgUrl = e.target.result;
                //     this.IntegrationOCR();
                // }
                // reader.readAsDataURL(file);
            }
        },
        IntegrationOCR() {
            // const serverEndPoint = "http://localhost:3000/perform-ocr";
            // fetch(serverEndPoint, {
            //     method: 'POST',
            //     headers: { 'content-type': 'application/json' },
            //     body: JSON.stringify({ imgUrl: "abdulkadirkhan" })
            // }).then((response) => response.json()) // Add return statement here
            //     .then((data) => {
            //         console.log('data...!!!???', data);
            //         this.recognizedText = data;
            //     }).catch((error) => {
            //         console.error('Error during fetch:', error);
            //     });
            const serverEndPoint = 'http://localhost:3000/perform-ocr';
            fetch(serverEndPoint, {
                method: 'POST',
                mode:'no-cors',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify({ imgUrl: this.imgUrl }),
            }).then((response) => response.json()).then((data) => {
                    // console.log('OCR Result:', data.recognizedText);
                    // this.recognizedText = data.recognizedText;
                    console.log('recognise text.......????????',data);
                }).catch((error) => {
                    console.error('Error during fetch:', error);
                });
        }
    }

}

</script>


<style scoped></style>