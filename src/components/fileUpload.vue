<template>
  <div>
    <input
      type="file"
      name="file"
      ref="myFileRef"
      multiple
      accept="/*image"
      @change="beforeUpload"
    >
    <button
      type="button"
      v-on:click="uploadFile()"
    >Upload</button>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'FileUpload',
  data() {
    return {
      file: "",
    }
  },
  methods: {
    beforeUpload() {
      this.file = this.$refs.myFileRef.files;
      
    },
    uploadFile: function () {
    console.log(this.file)
      let formData = new FormData();

      formData.append('img', this.file);
      for (let i = 0; i < this.file.length; i++) {
        formData.append("img", this.file[i]);
      }


    //   console.log(formData + (" formdata"))
      axios.post('http://localhost:3000/upload',
        formData
      ).then(res => {
        console.log(res.data);
        alert(res.data)
      })
        .catch(error => {
          console.error("file upload failed", error);
        });
    }
  }
}
</script>
