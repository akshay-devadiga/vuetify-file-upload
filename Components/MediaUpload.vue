<template>
  <v-card flat class="pa-2 media-file-btn">
    <input
      ref="mediaInput"
      type="file"
      :accept="accept"
      :multiple="multiple"
      :disabled="disabled"
      @change="uploadFile"
    >
    <v-text-field
      class="media-text-field"
      prepend-icon="attach_file"
      v-model="fileName"
      :label="label"
      :disabled="disabled"
      @click="showFileSelector"
      :outline="outline"
      v-if="variant===mediaInputType.vuetifyTwo"
    ></v-text-field>
    <v-btn
      v-else-if="variant===mediaInputType.browse"
      :disabled="disabled"
      :color="color"
      @click="showFileSelector"
    >
      <slot>Browse</slot>
    </v-btn>
  </v-card>
</template>

<script>
export default {
  props: {
    value: {
      type: File,
      default: null
    },
    accept: {
      type: String,
      default: ""
    },
    disabled: {
      type: Boolean,
      default: false
    },
    multiple: {
      type: Boolean,
      default: false
    },
    label: {
      type: String,
      default: "FileInput"
    },
    variant: {
      type: Number,
      default: 1
    },
    color: {
      type: String,
      default: "primary"
    },
    outline: {
      type: Boolean,
      default: true
    }
  },
  data() {
    return {
      fileName: "",
      mediaInputType: { browse: 2, vuetifyTwo: 1 }
    };
  },
  methods: {
    showFileSelector() {
      this.$refs.mediaInput.click();
    },
    uploadFile(e) {
      const file = e.target.files[0];
      if (file) {
        this.fileName = file.name;
        this.$emit("change", file);
      }
    }
  }
};
</script>

<style scoped>
.media-file-btn {
  display: inline-block;
}
.media-file-btn input[type="file"] {
  position: absolute;
  filter: alpha(opacity=0);
  opacity: 0;
}
</style>
<style>
.media-text-field .v-text-field__details {
  display: none;
}
</style>