<template >
  <div class="multi form-group">
    <label :for="id" class="font-size-sm font-weight-bold text-primary">{{
      label
    }}</label>
    <div class="d-flex">
      <div>
        <input
        :id="id"
        multiple
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
     <div class="flex-grow-1 mx-2" v-if="isUploading">
          <b-progress :value="uploadProgress" :max="100" show-progress animated />
     </div>
     <div class="d-flex flex-wrap mt-3">
         <img v-for="(uploadedImg) in uploadedImgs" :key="uploadedImg" :src="uploadedImg" alt="Alternative text for Uploaded Image" class="img-fluid img-thumbnail uploaded-img mr-2 mt-2">
     </div>
    </div>
  </div>
</template>
<script>
import API from "../../services";
import _ from "lodash";
export default {
  props: {
    label: {
      type: String,
      required: false,
      default: "Upload Multiple Files",
    },
    api:{
        type:String,
        required:true
    },
    id:{
        type:String,
        required: true
    }
  },
  data:() => ({
            uploadedImgs:[],
            isUploading: false,
            uploadProgress: 0
  }),
  methods: {
    async handleChange() {
      let files = this.$refs.uploadInput.files;
      let formData = new FormData();
      _.forEach(files,(file)=>{
          formData.append("files", file);
      });
      this.isUploading = true;
      let { data } = await API.post(this.api, formData,{
          onUploadProgress: ({total,loaded}) =>{
              this.uploadProgress = ((loaded/total)*100).toFixed(2);
          },
      });
      this.uploadedImgs = [...this.uploadedImgs, ...data];
      this.isUploading = false;
      this.uploadProgress = 0;
    },
  },
};
</script>
