<template>
  <v-app>
    <v-layout px-2 row wrap>
      <v-flex xs12 md12>
        <v-card>
          <media-upload accept="videos/*" @change="uploadFile"/>
        </v-card>
      </v-flex>
    </v-layout>
  </v-app>
</template>

<script>
import mediaUpload from "../Components/MediaUpload.vue";
export default {
  components: { mediaUpload },
  name: "App",
  data() {
    return {
      filename: ""
    };
  },
  methods: {
    uploadFile(e) {
      console.log(e);
    }
  }
};
</script>

<style type="text/css">
#card-parent-2 {
  position: relative;
}
.preview-card {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
</style>
