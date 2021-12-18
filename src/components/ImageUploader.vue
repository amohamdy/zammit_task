<template>
     <div class="upload-image-wrapper card">
       <!-- header -->
      <div class="upload-image-wrapper__head" v-if="checkedImages.length>0">
        <h3 >{{checkedImages.length+' ' +'Media Selected'}}</h3>
         <a class="custom" @click="onDelete">Delete Files</a>
        </div>
        <div class="upload-image-wrapper__head" v-else>
        <h3 >Media</h3>
        <a>Add media from URL</a>
      </div>

      <!-- image-wrapper -->
      <div class="upload-image-wrapper__content" v-if="selectedImages.length>0">
        <label class="image-wrapper image-wrapper--right border" for="image-0">
          <input type="checkbox" id="image-0" :value="selectedImages[0].name" v-model="checkedImages" />

          <img :src="selectedImages[0].src" >
        </label>
        <div class="image-wrapper image-wrapper--left" >
            <label v-for="(image, index) in selectedImages.slice(1)"  :key="index" class="image-wrapper--left__image border" :for="'image-'+`${index+1}`">
              <input type="checkbox" :id="'image-'+`${index+1}`" :value="image.name" v-model="checkedImages" />
              <img :src="image.src"/>
            </label>
        </div>
      </div>

      <!-- upload btn -->
      <div class="upload-image-wrapper__btn" :class="selectedImages.length>0?'custom':''">
        <img alt="Vue logo" src="../assets/download.png">
        <label for="upload-file">
          <input type="file" @Change="onFileSlected" id="upload-file" accept="image/*" multiple>
          Add Files</label>
          <span>or drop files to upload</span>
      </div>
    </div>
</template>

<script>
export default {
  name: 'ImageUploader',
 data() {
    return {selectedImages : [],
    checkedImages:[],
    title:'' }
  },
  methods:{
    onFileSlected(event){
      let files = event.target.files;
      for(let i =0; i<files.length; i++){
        let imageSrc= (window.URL || window.webkitURL).createObjectURL(files[i]);
          this.selectedImages.push({'name':files[i].name,'src': imageSrc} )
      }
    },
    onDelete(){
      this.selectedImages= this.selectedImages.filter(i => !this.checkedImages.find(j => j === i.name));
      this.checkedImages= []

    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "../scss/mixins.scss";
@import "../scss/variables.scss";

.upload-image-wrapper{
  .border{
    border: 1px solid $gray-100;
    border-radius: 11px;
    overflow: hidden;
    position: relative;
  }
  &__head{
    @include display-flex(row,space-between,center);
    a{
      color:$blue-100;
      &.custom{
        color:red;
        cursor: pointer;
      }
    }
  }
  &__btn{
    border-radius: 11px;
    border:1px dashed $blue-100;
    background-color:$blue-50;
    height:200px;
    @include display-flex(column, center,center);
    &.custom{
      width:25%;
      height: 130px;
      img{
        display:none;
      }
      label{
        border:0;
        background-color: transparent;
      }
    }
    label{
      border:1px solid gray;
      border-radius: 5px;
      padding:8px 16px;
      background-color: $gray-100;
      margin-bottom:10px;
    }
    input[type="file"]{
      position: absolute;
      visibility: hidden;
    }
  }
  &__content{
    height:500px;
    margin-bottom:15px;
     @include display-flex(row, space-between, flex-start);
    .image-wrapper{
      width:calc(100% / 2 - 5px);
      @include display-flex(row, flex-start, flex-start);
      height:100%;
      flex-wrap:wrap;
      input[type="checkbox"]{
        position: absolute;
        left:10px;
        top:10px;
        z-index:1;
      }

       img{
          object-fit: cover;
          width:100%;
          height: 100%;
        }
      &--left{
        &__image{
        width:calc(100% / 2 - 15px);
        height: calc(50% - 5px);
        display:flex;
        margin-inline:5px;
        &:nth-of-type(1), &:nth-of-type(2){
          margin-bottom: 5px;
        }
      }
      }
    }
  }
}


</style>
