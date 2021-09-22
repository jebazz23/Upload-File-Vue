<template >
    <div class="single form-group">
        <label  class="font-size-sm font-weight-bold text-primary">{{label}}</label>
        <input type="file" ref="uploadInput" @change="handleChange" class="form-control upload-input" />
        <div class="uploader-mask d-flex justify-content-center align-items-center">
                <img src="@/assets/upload.png" class="uploader-icon img-fluid" alt="">
        </div>
    </div>
</template>
<script>
export default {
    props:{
        label:{
            type:String,
            required: false,
            default: 'Upload Single File'
        }
    },
    methods:{
        handleChange(){
            console.log(this.$refs.uploadInput.files[0]);
        }
    }
}
</script>
