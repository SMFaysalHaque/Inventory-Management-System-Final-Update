<template>
    <div>
        <div class="assign-area border border-stone-300 rounded-sm w-[500px] ms-5 mt-3 px-1 py-1">
            <div class="flex w-auto">
                <input class="border rounded-lg contrast-more:border-slate-400 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500 px-1 me-1 w-full" type="search" name="" id="" placeholder="Search">
                <button class="border border-red-600 bg-red-600 text-white hover:bg-red-500 rounded-sm px-2" @click="$emit('closeAssignBtn')">
                    Close
                </button>
            </div>
            <div v-for="(singleProduct, i) in filterProduct" :key="singleProduct" class="">
                <div class="flex justify-between items-center py-1">
                    <!-- <p>{{ singleProduct.category }}</p> -->
                    <button @click="brandProductModal(singleProduct.category, i)" class="border border-green-700 bg-green-700 hover:bg-green-500 hover:border-green-500 rounded-sm text-white px-2">
                    add
                    </button>
                </div>
                {{ singleProduct.isActive }}
                <div v-if="singleProduct.isActive">
                    <AssignProductQty :selectedItemName="selectedItemName"/>
                </div>
            </div>
            
        </div>
    </div>
</template>

<script>
import AssignProductQty from './AssignProductQty.vue'
    export default {
        emits: ['closeAssignBtn'],
        components: {
            AssignProductQty
        },
        data() {
            return {
                // key: value
                products: [],
                filterProduct: [],
                selectedItemName: ''
                
            }
        },
        mounted () {
            this.products = JSON.parse(localStorage.getItem('setNewProduct'))
            // console.log("ALL PRODUCTS: ", this.products);
            // assign button filter
            const arrayOfItems = this.products.filter((item) => {
                return item.category
            })
            console.log("ARRAY OF ITEMS: ", arrayOfItems);
            this.filterProduct = Array.from(new Set(arrayOfItems));
            console.log('qqqqq: ', this.filterProduct);

        },
        methods: {
            addModel() {
                
            },
            closeModal(){
                this.$emit('closeAssignBtn')
            },
            brandProductModal(value,i){
                console.log('vvvv: ', value)
                console.log("Category:", value, "Index:", i);
                // console.log("product name",singleProduct)
                this.selectedItemName = value
                localStorage.setItem('setNewProduct', JSON.stringify(this.products))
                // console.log("xxxx", this.products, i);
                this.singleProduct.isActive = true
                console.log("gggg: ", this.singleProduct.isActive, i);
            },
            brandShowed(i){
                console.log("bbbb: ", brandShowed);
            },
            singleProduct(){
                console.log(this.products);
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>