<template>
        <div class="form-group d-flex">
            <label for="title" class="mb-2 text-left" >{{label}}
                <input  v-if="number" :value="quantity" :placeholder="placeholder" id="title" class="form-control" type="number"/>
                <span v-else-if="pricing" class="d-flex form-control custom">
                    EGP
                    <input :value="price" :placeholder="placeholder" id="price" />
                </span>
                <input v-else :value="title" :placeholder="placeholder" id="title" class="form-control"/>

            </label>

        </div>


</template>



<script>
    export default{
         name: 'TextInput',

         props:['placeholder', 'label', 'number', 'pricing', 'title', 'quantity', 'price'],
    }
</script>


<style scoped lang="scss">


.form-group{
    flex-direction:column;
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
