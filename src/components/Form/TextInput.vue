<template>
        <div class="form-group d-flex flex-column">
            <label  class="mb-2 text-left" >{{label}}
                <input  v-if="number" :value="modelValue" :placeholder="placeholder"  class="form-control" type="number" @input="$emit('update:modelValue', $event.target.value)"/>
                <span v-else-if="pricing" class="d-flex form-control custom">
                    EGP
                    <input :value="modelValue" :placeholder="placeholder" @input="$emit('update:modelValue', $event.target.value)"/>
                </span>
                <input v-else :value="modelValue" :placeholder="placeholder"  class="form-control" @input="$emit('update:modelValue', $event.target.value)"/>
            </label>
        </div>
</template>



<script>
    export default{
         name: 'TextInput',
         props:['placeholder', 'label', 'number', 'pricing', 'modelValue'],
    }
</script>


<style scoped lang="scss">


.form-group{
    label{
       width:100%;
    }
    input{
        height: 30px;
        width:100%;
    }
    .custom{
        align-items: center;
        input{
            border:0;
        }
    }
}


</style>
