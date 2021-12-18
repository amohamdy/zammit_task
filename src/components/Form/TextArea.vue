<template>
       <div class="form-group d-flex flex-column">
            <label for="description" class="mb-2">Description</label>
            <textarea :value="modelValue" placeholder="Description"  id="description" rows="5"  class="form-control" @input="$emit('update:modelValue', $event.target.value)"></textarea>
        </div>
</template>


<script>
export default {
    name:'TextArea',
    props:['modelValue'],

}
</script>

<style lang="scss" scoped>
    textarea{
        resize:none;
    }
</style>