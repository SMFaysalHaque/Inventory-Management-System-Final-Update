<template>
    <div>
        <div class="assign-area border border-stone-300 rounded-sm w-[500px] ms-5 mt-3 px-1 py-1">
            <div class="flex w-auto">
                <input class="border rounded-lg contrast-more:border-slate-400 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500 px-1 me-1 w-full" type="search" name="" id="" placeholder="Search">
                <button class="border border-red-600 bg-red-600 text-white hover:bg-red-500 rounded-sm px-2" @click="$emit('closeAssignBtn')">
                    Close
                </button>
            </div>
            <div v-for="(singleProduct, i) in uniq" :key="singleProduct" class="">
                <div class="flex justify-between items-center py-1">
                    <p>{{ singleProduct }}</p>
                    <button @click="brandProductModal(i)" class="border border-green-700 bg-green-700 hover:bg-green-500 hover:border-green-500 rounded-sm text-white px-2">
                    add
                    </button>
                </div>
                <div v-if="isBrandProductVisible">
                    <AssignProductQty />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import AssignProductQty from './AssignProductQty.vue'
    export default {
        emits: ['closeAssignBtn', ''],
        components: {
            AssignProductQty
        },
        data() {
            return {
                // key: value
                products: [],
                isBrandProductVisible: false,
                uniq: []
            }
        },
        mounted () {
            this.products = JSON.parse(localStorage.getItem('setNewProduct'))
            const arrayOfItems = this.products.map((item) => {
                return item.category
            })
            this.uniq = Array.from(new Set(arrayOfItems));
        },
        methods: {
            addModel() {
                
            },
            closeModal(){
                // this.$emit('closeAssignBtn')
            },
            brandProductModal(i){
                this.isBrandProductVisible = true
                localStorage.setItem('setNewProduct', JSON.stringify(this.products))
                console.log("xxxx", this.products[i]);
            },
            singleProduct(){
                console.log(this.products);
            }
            
        },
    }
</script>

<style lang="scss" scoped>

</style>