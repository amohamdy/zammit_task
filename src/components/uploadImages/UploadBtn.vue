<template>
    <div class="upload-image-wrapper__btn" :class="selectedImages.length>0?'custom':''">
        <img alt="Vue logo" src="../../assets/download.png">
        <label for="upload-file">
          <input type="file" @Change="$emit('selected-files', $event)" id="upload-file" accept="image/*" multiple>
          Add Files</label>
          <span>or drop files to upload</span>
    </div>

</template>


<script>
    export default{
        name:'UploadBtn',
        props:['selectedImages']
    }

</script>
<style lang="scss" scoped>
@import "../../scss/variables.scss";
@import "../../scss/mixins.scss";


  .upload-image-wrapper__btn{
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
</style>

