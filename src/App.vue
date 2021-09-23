<template>
  <div id="app" class="d-flex flex-column">
    <Navbar />
    <div class="container flex-grow-1 mt-5 mb-5 py-2">
      <div class="row">
        <div class="col-md-6 col-sm-12 mx-auto">
          <div class="card">
            <div class="card-header">
              <h3 class="text-primary font-weight-bold font-size-lg">
                Upload your file
              </h3>
            </div>
             <div class="card-body">
            <form>
              <SingleUploader 
              id="single-file-upload" 
              label="Upload File Here..." 
              api="images/single-upload"/>
              <MultiUploader 
              id="multi-file-upload" 
              label="Upload Multiple Files Here..." 
              api="images/multi-upload"/>
            </form>
          </div>
          </div>
        </div>
      </div>
    </div>
    <Footer />
  </div>
</template>

<script>
import Navbar from "./components/Layouts/Navbar.vue";
import Footer from "./components/Layouts/Footer.vue";
import SingleUploader from "./components/Uploader/SingleUploader.vue";
import MultiUploader from "./components/Uploader/MultipleUploader.vue"
export default {
  name: "App",
  components: {
    Navbar,
    Footer,
    SingleUploader,
    MultiUploader
  },
};
</script>
