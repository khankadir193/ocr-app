<template>
  <div>
    <input type="file" @change="handleUploadFile">
    <button @click="submitImage">Submit</button>
  </div>
</template>
  
<script>
export default {
  name: "FileUploadOCR",
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

        console.log('formData...???',formData);

        if(this.selectedFile){
        const res = await this.convertDataImgUrl(this.selectedFile);
        console.log('res.....??????????',res);
        }
       
        //this code calling backend to get the content of upload images..
        const serverEndPoint = 'http://localhost:4000/upload';

        const response = await fetch(serverEndPoint, {
          method: 'POST',
          body: this.selectedFile,
          mode:'no-cors'
        });

        const result = await response.json();
        console.log('result...????????', result);
      } catch (error) {
        console.error('Error uploading image:', error);
      }
    },
    convertDataImgUrl(file) {
      const reader = new FileReader();

      reader.onload = (e) => {
        this.imageUrl = e.target.result;
      };

      // Read the file as a data URL
     return reader.readAsDataURL(file);
    }
  }
};
</script>
  