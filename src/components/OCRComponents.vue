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
            console.log('event...???',event.target.files[0]);
            const file = event.target.files[0].name; 
            if(file){
                const reader = new FileReader();
                reader.onload = (e)=>{
                    console.log('e.target.result',e.target.result);
                    this.imgUrl = e.target.result;
                    this.IntegrationOCR();
                }
            // reader.readDataURL(file);

            }
        },
        IntegrationOCR(){
            console.log('backend-ocr integration');
        }
    }

}

</script>


<style scoped></style>