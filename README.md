## Vuetify 1.5 Simple File Upload Component

This is simplest file upload component built using Vuetify1.5.

```vue
<template>
.
.
 <c-file-upload accept="videos/*" @change="uploadFile"/>
.
.
</template>
<script>
import CFileUpload from "../Components/CustomFileUpload.vue";
export default {
  components: { CFileUpload },
  name: "App",
  data() {
    return {
      filename: ""
    };
  },
  methods: {
    uploadFile(e) {
      console.log(e);
      //Uploaded File can be accesed here 
    }
  }
};
</script>
```

## File-Input Component.vue

```vue
<template>
  <v-layout class="pa-2 media-file-btn">
    <input
      ref="fileInput"
      type="file"
      :accept="accept"
      :multiple="multiple"
      :disabled="disabled"
      @change="uploadFile"
    >
    <v-flex xs3 sm4 md2 v-if="variant===fileInputType.vuetifyTwo">
      <v-text-field
        prepend-icon="attach_file"
        v-model="fileName"
        :label="label"
        :disabled="disabled"
        @click="showFileSelector"
        :outline="outline"
      ></v-text-field>
    </v-flex>
    <v-flex xs3 sm4 md2 v-else-if="variant===fileInputType.browse">
      <v-btn :disabled="disabled" :color="color" @click="showFileSelector">
        <slot>Browse</slot>
      </v-btn>
    </v-flex>
    <v-flex xs3 sm4 md2 if="variant===fileInputType.browse" class="text-xs-center">
      <v-chip v-if="fileName" class="ma-2" disabled>{{fileName}}</v-chip>
    </v-flex>
  </v-layout>
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
      default: 2
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
      fileInputType: { browse: 2, vuetifyTwo: 1 }
    };
  },
  methods: {
    showFileSelector() {
      this.$refs.fileInput.click();
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
```


## Props


|                |Description                           
|----------------|-------------------------------
|Variant|`There are two variants(Normal/Vuetify2) : 1-vuetify2 / 2-Normal`
|accept|`accepts file types for input : audio/* video/* image/*`            
|disabled          |`disables file input component (button/textfield/input) :true / false  `            
|multiple|`To accept multiple files: true/false`
|label |`To accept custom label name in case of vuetify2 variant : FileInput / Custom name` 
|color|`By default it is primary to set just pass color directly`
|Outline |`In case of variant 1 this will be set by default : true/false`


## License
[MIT](https://choosealicense.com/licenses/mit/)
