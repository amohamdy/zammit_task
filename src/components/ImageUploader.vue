<template>
  <div class="upload-image-wrapper card">
    <!-- header -->
    <div class="upload-image-wrapper__head" v-if="checkedImages.length > 0">
      <h3>{{ checkedImages.length + " " + "Media Selected" }}</h3>
      <a class="custom" @click="onDelete">Delete Files</a>
    </div>
    <div class="upload-image-wrapper__head" v-else>
      <h3>Media</h3>
      <a>Add media from URL</a>
    </div>

    <!-- image-wrapper -->
    <div class="upload-image-wrapper__content" v-if="selectedImages.length > 0">
      <!-- <label class="image-wrapper image-wrapper--right border" for="image-0">
        <input
          type="checkbox"
          id="image-0"
          :value="selectedImages[0].name"
          v-model="checkedImages"
        />

        <img :src="selectedImages[0].src" />
      </label> -->

      <div class="image-wrapper image-wrapper--left">
        <draggable
          class="dragArea list-group w-full d-flex"
          v-model="selectedImages"
        >
          <label
            v-for="(image, index) in selectedImages"
            :key="index"
            class="image-wrapper--left__image border"
            :for="'image-' + `${index}`"
          >
            <input
              type="checkbox"
              :id="'image-' + `${index}`"
              :value="image.name"
              v-model="checkedImages"
            />
            <img :src="image.src" />
          </label>
        </draggable>
      </div>
    </div>

    <!-- upload btn -->
    <UploadBtn
      :selectedImages="selectedImages"
      @selected-files="onFileSlected"
    />
  </div>
</template>

<script>
import UploadBtn from "./uploadImages/UploadBtn.vue";
import { VueDraggableNext } from "vue-draggable-next";
export default {
  name: "ImageUploader",
  components: { UploadBtn, draggable: VueDraggableNext },

  data() {
    return {
      selectedImages: [],
      checkedImages: [],
      title: "",
    };
  },
  methods: {
    onFileSlected(event) {
      let files = event.target.files;
      for (let i = 0; i < files.length; i++) {
        let imageSrc = (window.URL || window.webkitURL).createObjectURL(
          files[i]
        );
        this.selectedImages.push({ name: files[i].name, src: imageSrc });
      }
    },
    onDelete() {
      this.selectedImages = this.selectedImages.filter(
        (i) => !this.checkedImages.find((j) => j === i.name)
      );
      this.checkedImages = [];
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "../scss/mixins.scss";
@import "../scss/variables.scss";
.dragArea {
  height: 100%;
}

.upload-image-wrapper {
  .border {
    border: 1px solid $gray-100;
    border-radius: 11px;
    overflow: hidden;
    position: relative;
  }
  &__head {
    @include display-flex(row, space-between, center);
    a {
      color: $blue-100;
      &.custom {
        color: red;
        cursor: pointer;
      }
    }
  }

  &__content {
    height: 500px;
    margin-bottom: 15px;
    @include display-flex(row, space-between, flex-start);
    position: relative;

    .image-wrapper {
      width: calc(100% / 2 - 5px);
      @include display-flex(row, flex-start, flex-start);
      margin-left: auto;
      height: 100%;
      input[type="checkbox"] {
        position: absolute;
        left: 10px;
        top: 10px;
        z-index: 1;
      }

      &--left {
        &__image {
          width: calc(100% / 2 - 15px);
          height: calc(50% - 5px);
          display: flex;
          margin-inline: 5px;
          &:nth-of-type(1),
          &:nth-of-type(2) {
            margin-bottom: 5px;
          }
          &:nth-of-type(1) {
            position: absolute;
            left: 0;
            height: 100%;
          }
        }
      }
    }
  }
}
</style>
