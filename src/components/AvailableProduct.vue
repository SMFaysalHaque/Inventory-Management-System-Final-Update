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
                    <tr v-for="x in eachProduct" :key="x">
                        <td class="border border-slate-200 text-center">{{ x.itemCategory }}</td>
                        <td class="border border-slate-200 text-center">{{ x.itemBrand }}</td>
                        <td class="border border-slate-200 text-center">{{ x.itemModel }}</td>
                        <td class="border border-slate-200 text-center">{{ x.countModelAvailableProduct }}</td>
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
                availableProduct: [],
                eachProduct: []
            }
        },
        mounted () {
            // get localStorage
            this.availableProduct = JSON.parse(localStorage.getItem('allProductsCategories')) ? JSON.parse(localStorage.getItem('allProductsCategories')) : []
            console.log("Available Product:", this.availableProduct);
            this.employeeItemMapping = JSON.parse(localStorage.getItem('employeeItemMapping')) ? JSON.parse(localStorage.getItem('employeeItemMapping')) : []
            console.log("Employee Mapping:", this.employeeItemMapping);

            for(let i = 0; i < this.availableProduct.length; i++){
                for(let j = 0; j < this.availableProduct[i].items.length; j++){
                    let element = this.availableProduct[i].items[j]
                    console.log("XXX", element);
                    this.eachProduct.push(element)
                    console.log("TTTTHHHH:", this.eachProduct);
                }
            }

            // relation with this.availableProduct and this.employeeItemMapping
            this.eachProduct.forEach((el1, index1) => {
                let reserveModel = el1.itemModel;
                let totalTaken = 0;
                this.employeeItemMapping.filter((el2, index2) => {
                    if(reserveModel === el2.itemModel){
                        totalTaken = totalTaken + el2.itemQuantity
                    }
                })
                el1.countModelAvailableProduct = el1.itemQuantity - totalTaken
                console.log(typeof el1.countModelAvailableProduct);
                console.log(typeof el1.countModelAvailableProduct);
                console.log(typeof el1.countModelAvailableProduct);
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