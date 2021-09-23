<template >
  <div class="drop-zone form-group">
    <label :for="id" class="font-size-sm font-weight-bold text-primary">{{
      label
    }}</label>
    <div class="d-flex">
 
      <input
        :id="id"
        type="file"
        ref="uploadInput"
        @change="handleChange"
        class="form-control upload-input"
      />
      <div
        class="
          uploader-mask
          d-flex
          justify-content-center
          flex-column
          align-items-center
          
        "
      >
        <img src="@/assets/upload.png" class="uploader-icon img-fluid" alt="" />
        <p class="text-muted font-size-sm">Upload Your files here...</p>
      </div>
     
    </div>
    <div class="d-flex mt-3" v-if="isUploading">
      <div class="flex-grow-1 mx-2">
        <b-progress :value="uploadProgress" :max="100" show-progress animated />
      </div>
    </div>
    <div class="d-flex flex-wrap mt-3">
      <img
        v-for="uploadedImg in uploadedImgs"
        :key="uploadedImg"
        :src="uploadedImg"
        alt="Alternative text for Uploaded Image"
        class="img-fluid img-thumbnail uploaded-img mr-2 mt-2"
      />
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
    api: {
      type: String,
      required: true,
    },
    id: {
      type: String,
      required: true,
    },
  },
  data: () => ({
    uploadedImgs: [],
    isUploading: false,
    uploadProgress: 0,
  }),
  methods: {
    async handleChange() {
      let file = this.$refs.uploadInput.files[0];
      let formData = new FormData();
      formData.append("file", file);
      this.isUploading = true;
      let { data } = await API.post(this.api, formData, {
        onUploadProgress: ({ total, loaded }) => {
          this.uploadProgress = ((loaded / total) * 100).toFixed(2);
        },
      });
      this.uploadedImgs = [...this.uploadedImgs, data.imagePath];
      this.isUploading = false;
      this.uploadProgress = 0;
    //   this.$refs.uploadInput.value = "";
    },
  },
};
</script>
