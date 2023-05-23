<template>
    <div>
        <div class="flex items-center justify-between my-2.5">
            <p class="font-bold text-lg">Unit Types</p>
            <button @click="showModal()" class="border border-green-700 bg-green-700 hover:bg-green-500 hover:border-green-500 rounded-sm text-white px-10 py-2">Add New Unit</button>
        </div>

        <!-- addnewunit emit start here -->
        <div class="py-2" v-if="isModalVisible">
            <Addnewunit @addNewProduct="getProductData" @close='closeModal()'/>
        </div>
        <!-- addnewunit emit end here -->
        
        <div class="grid grid-cols-6 bg-slate-100 border border-cyan-700">
            <div class="col-span-2 flex justify-center items-center p-2">
                <p>Type</p>
            </div>
            <div class="col-span-4 flex justify-center items-center border p-2">
                <p>Details</p>
            </div>
        </div>
        <div v-for="(allProductDetail, i) in allProductDetails" :key="allProductDetail.i" class="grid grid-cols-6 border border-cyan-700">
            <div class="col-span-2 flex justify-center items-center border-e-2">
                <p>{{ allProductDetail.type }}</p>
            </div>
            <div class="col-span-4 flex flex-col justify-center ps-10 py-10 space-y-3">
                <p>Model Name: {{ allProductDetail.model }}</p>
                <p>Quantity: {{ allProductDetail.quantity }}</p>
            </div>
        </div>
    </div>
</template>


<script>
import Addnewunit from '../components/addnewunit.vue';
// import { useStore } from '@nanostores/vue';
// import { prodcutDetails } from '../Store/store.js';
    export default {
        components: {
            Addnewunit,
        },
        data() {
            return {
                isModalVisible: false,
                // allProductDetails: prodcutDetails.get(), //when we use useStore(productDetails) on that time storage array is only read able or muted. But when we use "productDetails.get()" on that time storage's array is read able or muted.
                allProductDetails: [],
            }
        },
        mounted () {
            let arr = localStorage.getItem('allProductDetails')
            this.allProductDetails = JSON.parse(arr) ? JSON.parse(arr) : [];
        },
        methods: {
            showModal() {
                this.isModalVisible = true;
            },
            closeModal() {
                this.isModalVisible = false;
            },
            getProductData(value){
                this.allProductDetails.push(value);
                localStorage.setItem('allProductDetails', JSON.stringify(this.allProductDetails))
                console.log(value);
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>