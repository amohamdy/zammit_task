<template>
       <div class="form-group d-flex flex-column" >
            <label for="description" class="mb-2">Description</label>
            <!-- <textarea  placeholder="Description"  id="description" rows="5"  class="form-control" @input="$emit('update:modelValue', $event.target.value)"></textarea> -->
            <vue-editor :modelValue="modelValue" v-model="description" @text-change="$emit('update:modelValue',description )"></vue-editor>
        </div>
</template>


<script>
import { VueEditor } from "vue3-editor";

export default {
    name:'TextArea',
    props:['modelValue'],
    components: {
    VueEditor
  },
  data(){
      return{
          description:''

      }
  }


}
</script>

<style lang="scss" scoped>
    textarea{
        resize:none;
    }
</style>