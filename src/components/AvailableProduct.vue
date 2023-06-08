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
                    <tr v-for="availableSingleProduct in setNewProduct" :key="availableSingleProduct">
                        <td class="border border-slate-200 text-center">{{ availableSingleProduct.category }}</td>
                        <td class="border border-slate-200 text-center">{{ availableSingleProduct.brand }}</td>
                        <td class="border border-slate-200 text-center">{{ availableSingleProduct.model }}</td>
                        <td class="border border-slate-200 text-center">{{ availableSingleProduct.countAvailableProduct }}</td>
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
                setNewProduct: [],
                availableProduct: []
            }
        },
        mounted () {
            // get localStorage
            this.setNewProduct = JSON.parse(localStorage.getItem('setNewProduct')) ? JSON.parse(localStorage.getItem('setNewProduct')) : []
            console.log("Set New Product:", this.setNewProduct);
            this.employeeItemMapping = JSON.parse(localStorage.getItem('employeeItemMapping')) ? JSON.parse(localStorage.getItem('employeeItemMapping')) : []
            console.log("Employee Item Mapping", this.employeeItemMapping);

            // relation with this.setNewProduct and this.employeeItemMapping
            this.setNewProduct.forEach((item) => {
                let reserveModel = item.model;
                let reserveQuantity = item.quantity;
                console.log("Model:", reserveModel, "Reserve Quantity:", reserveQuantity);
            })
            this.setNewProduct.forEach((el1, index1) => {
                let reserveBrand = el1.brand;
                let reserveModel = el1.model;
                let totalTaken = 0;
                // console.log("Reserve Model:", reserveBrand, "||", "Reserve Model:", reserveModel);
                this.employeeItemMapping.filter((el2, index2) => {
                    if(reserveModel === el2.itemModel){
                        // console.log(el2.itemQuantity);
                        totalTaken = totalTaken + el2.itemQuantity
                        console.log(totalTaken);
                    }
                })
                el1.countAvailableProduct = el1.quantity - totalTaken
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