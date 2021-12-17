<template>
       <div class="form-group d-flex">
            <label for="description" class="mb-2">Description</label>
            <textarea :value="desc" placeholder="Description"  id="description" rows="5"  class="form-control"></textarea>
        </div>
</template>


<script>
export default {
    name:'TextArea',
    data(){
        return{

        }
    },
    props:['desc'],

}
</script>

<style lang="scss" scoped>
    .d-flex{
        flex-direction:column
    }
    textarea{
        resize:none;
    }
</style>