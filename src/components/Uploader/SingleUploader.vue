<template >
  <div class="single form-group">
    <label :for="id" class="font-size-sm font-weight-bold text-primary">{{
      label
    }}</label>
    <div class="d-flex">
      <div>
        <input
        :id="id"
          type="file"
          ref="uploadInput"
          @change="handleChange"
          class="form-control upload-input"
        />
        <div
          class="uploader-mask d-flex justify-content-center align-items-center"
        >
          <img
            src="@/assets/upload.png"
            class="uploader-icon img-fluid"
            alt=""
          />
        </div>
      </div>
      <img v-if="uploadedImg" :src="uploadedImg" class="img-fluid img-thumbnail ml-3 uploaded-img"  alt="Alternative text form Uploaded Image">

     <div class="flex-grow-1 mx-2" v-if="isUploading">
          <b-progress :value="uploadProgress" :max="100" show-progress animated />
     </div>
    </div>
  </div>
</template>
<script>
import API from "../../services";

export default {
  props: {
    label: {
      type: String,
      required: false,
      default: "Upload Single File",
    },
    api:{
      type:String,
      required: true
    },
    id:{
      type:String, 
      required:true
    }
  },
  data:() => ({
            uploadedImg:'',
            isUploading: false,
            uploadProgress: 0
  }),
  methods: {
    async handleChange() {
      let file = this.$refs.uploadInput.files[0];
      let formData = new FormData();
      formData.append("file", file);
      this.isUploading = true;
      let { data } = await API.post(this.api, formData,{
          onUploadProgress: ({total,loaded}) =>{
              this.uploadProgress = ((loaded/total)*100).toFixed(2);
          },
      });
      this.uploadedImg = data.imagePath;
      this.isUploading = false;
      this.uploadProgress = 0;
    },
  },
};
</script>
