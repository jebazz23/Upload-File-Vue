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
              <SingleUploader label="Upload File Here..." />
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
export default {
  name: "App",
  components: {
    Navbar,
    Footer,
    SingleUploader,
  },
};
</script>
