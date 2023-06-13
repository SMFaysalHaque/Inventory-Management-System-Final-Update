<template>
    <div>
        <div class="w-full bg-gray-100 h-screen my-5 rounded-md">
            <p class="font-bold text-md ms-5 pt-5">Available Products</p>
            <table class="table-auto w-[90%] mx-auto mt-5 border-collapse border border-slate-300">
                <thead>
                    <tr class="h-10 bg-gray-300 border-b-2 border-gray-400">
                        <th class="border border-slate-200">Category</th>
                        <th class="border border-slate-200">Brand</th>
                        <th class="border border-slate-200">Model</th>
                        <th class="border border-slate-200">Available Quantity</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="availableSingleProduct in availableProduct" :key="availableSingleProduct">
                        <td class="border border-slate-200 text-center">{{ availableSingleProduct.category }}</td>
                        <td class="border border-slate-200 text-center">{{ availableSingleProduct.brand }}</td>
                        <td class="border border-slate-200 text-center">{{ availableSingleProduct.model }}</td>
                        <td class="border border-slate-200 text-center">{{ availableSingleProduct.countModelAvailableProduct }}</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                // key: value
                employeeItemMapping: [],
                availableProduct: []
            }
        },
        mounted () {
            // get localStorage
            this.availableProduct = JSON.parse(localStorage.getItem('setNewProduct')) ? JSON.parse(localStorage.getItem('setNewProduct')) : []
            console.log("Available Product:", this.availableProduct);
            this.employeeItemMapping = JSON.parse(localStorage.getItem('employeeItemMapping')) ? JSON.parse(localStorage.getItem('employeeItemMapping')) : []

            // relation with this.availableProduct and this.employeeItemMapping
            this.availableProduct.forEach((el1, index1) => {
                let reserveModel = el1.model;
                let totalTaken = 0;

                this.employeeItemMapping.filter((el2, index2) => {
                    if(reserveModel === el2.itemModel){
                        totalTaken = totalTaken + el2.itemQuantity
                    }
                })
                el1.countModelAvailableProduct = el1.quantity - totalTaken
            })
        },
        methods: {
            name() {
                
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>