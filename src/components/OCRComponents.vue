<template>
    <div>
        <input type="file" @change="handleUploadFile">
        <img :src="imgUrl" alt="Uploaded Image">
    </div>
</template>

<script>
export default {
    name: 'OCRComponents',
    data() {
        return {
            imgUrl: '',
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
            // const serverEndPoint = "http://localhost:3000/perform-ocr"
            // // console.log('jjj')
            // fetch(serverEndPoint, {
            //     method: 'POST', headers: { 'content-type': 'application/json' },
            //     body: JSON.stringify({ imgUrl: this.imgUrl })
            // }).then((response)=>{
            //     response.json();
            // }).then((data)=>{
            //     console.log('data...!!!???',data);
            //     this.recognizedText = data;
            // });

            const serverEndPoint = "http://localhost:3000/perform-ocr";

            fetch(serverEndPoint, {
                method: 'POST',
                headers: { 'content-type': 'application/json' },
                body: JSON.stringify({ imgUrl: "abdulkadirkhan" })
            })
                .then((response) => response.json()) // Add return statement here
                .then((data) => {
                    console.log('data...!!!???', data);
                    this.recognizedText = data;
                })
                .catch((error) => {
                    console.error('Error during fetch:', error);
                });

        }
    }

}

</script>


<style scoped></style>