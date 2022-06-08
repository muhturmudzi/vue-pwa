<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <input id="fileUpload" type="file" required accept="image/png, image/jpg, image/jpeg, image/webp" @change="uploadedImage">
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'HomeView',
  components: {
    HelloWorld
  },
  methods: {
    uploadedImage (e) {
      console.log(e.target.files[0], e)
      let type = e.target.files[0].type

      if (!type.match('image/png') && !type.match('image/jpg') && !type.match('image/jpeg') && !type.match('image/webp')) {
        alert('tipe file tidak sesuai')
      }

      const image = new Image();

      image.onload = function() {
          alert("The image width is " +this.width + " and image height is " + this.height)
      }

      image.src = window.URL.createObjectURL(e.target.files[0])
    }
  }
}
</script>
