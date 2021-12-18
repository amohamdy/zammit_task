<template>
<!-- first-card  -->
   <div class="form-wrapper card">
        <h3 class="mb-4 text-left">Inventory</h3>
        <div class="d-flex">
            <div class="text-input-wrapper">
                <TextInput placeholder="" label="SKU (Stock Keeping Unit)"/>
            </div>
            <div class="text-input-wrapper">
                <TextInput placeholder="" label="Barcode (ISBN, UPC, GTIN, etc.)"/>
            </div>
        </div>


        <div class="d-flex flex-column">
            <div>
                <input type="checkbox" id="track_quantity" v-model="track_quantity" checked />
                <label for="track_quantity">Track Quantity</label>
            </div>
            <div>
                <input type="checkbox" id="selling"  v-model="selling" />
                <label for="selling">Continue selling when out of stock</label>
            </div>

        </div>



        <hr/>
        <h3 class="mb-4 text-left">QUANTITY</h3>
            <div class="text-input-wrapper">
                <TextInput placeholder="0" label="Available" number="true" v-model="quantity"/>
            </div>

    </div>
<!-- second card -->
    <div class="form-wrapper card">
        <TextInput placeholder="Title" label="Title" v-model="productName"/>
        <TextArea v-model="description"/>
    </div>

<!-- third card -->
    <div class="form-wrapper card">
        <h3 class="mb-4 text-left">Pricing</h3>
        <div class="d-flex">
            <div class="text-input-wrapper">
                <TextInput placeholder="" label="Price" pricing="true" v-model="price"/>
            </div>
            <div class="text-input-wrapper">
                <TextInput placeholder="" label="Compare at price" pricing="true" v-model="compare_at_price"/>
            </div>
        </div>
        <hr>

        <div class="d-flex align-items-center">
            <div class="text-input-wrapper">
                <TextInput placeholder="" label="Cost per item" pricing="true" v-model="cost_per_item"/>
            </div>
            <div class="text-input-wrapper d-flex">
                <div class="d-flex flex-column">
                    <span>Margin</span>
                    <span>EGP {{margin}}</span>
                </div>
                <div class="d-flex flex-column">
                    <span>profit</span>
                    <span>EGP {{profit}}</span>

                </div>
            </div>

        </div>


    <div class="d-flex flex-column">

        <div>
            <input type="checkbox" id="change_tax"  v-model="changeTax" checked />
            <label for="change_tax">Change tax on this product</label>
        </div>

    </div>
    </div>

</template>



<script>
import TextInput from './Form/TextInput.vue';
import TextArea from './Form/TextArea.vue';
// import CheckBox from './Form/CheckBox.vue';
    export default{
         name: 'FormComponent',
         components:{
            TextInput,
            TextArea,
            // CheckBox
         },

        data(){
             return{
                 productName:'',
                 description:'',
                 quantity:'',
                 track_quantity:true,
                 selling:false,
                 changeTax:false,
                 margin:'',
                 profit:'',
                 price:'',
                compare_at_price:'',
                cost_per_item:''
             }
         },
         methods:{
            getIntialFormData(){
                const url = `https://61bc86bdd8542f00178247d6.mockapi.io/ecommerce/1`;
                this.axios.get(url).then((res) => {
                    console.log(res)
                    this.description=res.data.description;
                    this.productName = res.data.title;
                    this.quantity = res.data.quantity;
                    this.margin=res.data.margin;
                    this.profit=res.data.profit;
                    this.price=res.data.price;
                    this.compare_at_price=res.data.compare_at_price;
                    this.cost_per_item=res.data.cost_per_item

                }).catch(err=>console.log(err))
            },
         },
        mounted() {


            this.getIntialFormData()
        }

    }
</script>


<style scoped lang="scss">
@import "../scss/variables.scss";

.d-flex{
    justify-content: space-between;

}
.text-input-wrapper{
    width:calc(100% / 2 - 1rem)
}



</style>
