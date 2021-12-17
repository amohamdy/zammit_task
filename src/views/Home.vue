<template>
  <div>
      <ImageUploader></ImageUploader>
      <FormComponent></FormComponent>

  </div>


</template>


<script>
import ImageUploader from '@/components/ImageUploader.vue'
import FormComponent from '@/components/FormComponent.vue'

export default {
  name: 'Home',
  components: {
    ImageUploader,
    FormComponent
  }
}

</script>
