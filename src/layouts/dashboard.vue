<template>

    <div class="dashboard-area">
        <div class="grid grid-cols-2 max-xl:grid-cols-1 w-full bg-gray-100 p-5 rounded-md my-2.5">
            <div class="mx-1">
                <p class="text-center border border-slate-200 p-2 bg-gray-300">All Units</p>
                <div class="text-center border border-slate-200 p-2">
                    <table class="border-collapse border border-slate-400 w-full">
                        <thead>
                                <tr>
                                    <th class="border border-slate-300 bg-blue-100 w-1/12 py-2 text-center">Status</th>
                                    <th class="border border-slate-300 bg-blue-100 w-2/12 py-2 text-center">Category</th>
                                    <th class="border border-slate-300 bg-blue-100 w-2/12 py-2 text-center">Brand</th>
                                    <th class="border border-slate-300 bg-blue-100 w-2/12 py-2 text-center">Model</th>
                                    <th class="border border-slate-300 bg-blue-100 w-2/12 py-2 text-center">Quantity</th>
                                    <th class="border border-slate-300 bg-blue-100 w-3/12 py-2 text-center">Assign To</th>
                                </tr>
                        </thead>
                        <tbody>
                                <tr  v-for="singleEmployeeAssignUnit in employeesAssignUnits" :key="singleEmployeeAssignUnit">
                                    <td class="border border-slate-300 text-center py-3">Taken</td>
                                    <td class="border border-slate-300 text-center py-3">{{ singleEmployeeAssignUnit.itemCategory }}</td>
                                    <td class="border border-slate-300 text-center py-3">{{ singleEmployeeAssignUnit.itemBrand }}</td>
                                    <td class="border border-slate-300 text-center py-3">{{ singleEmployeeAssignUnit.itemModel }}</td>
                                    <td class="border border-slate-300 text-center py-3">{{ singleEmployeeAssignUnit.itemQuantity }}</td>
                                    <td class="border border-slate-300 text-center py-3">{{ singleEmployeeAssignUnit.employeeName }}</td>
                                </tr>
                        </tbody>
                    </table>
                </div>
            </div>
            <div class="mx-1">
                <p class="text-center border border-slate-200 p-2 bg-gray-300">Product Summary</p>
                <div class="text-center border border-slate-200 p-2">
                    <table class="border-collapse border border-slate-400 w-full">
                            <thead>
                                <tr>
                                    <th class="border border-slate-300 w-80 py-2 bg-blue-100">Category</th>
                                    <th class="border border-slate-300 w-80 py-2 bg-blue-100">Total Quantity</th>
                                    <th class="border border-slate-300 w-64 py-2 bg-blue-100"><a href="/AvailableProduct/">Available</a></th>
                                    <th class="border border-slate-300 w-64 py-2 bg-blue-100"><a href="/TakenProduct/">Taken</a></th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="singleProductSummary in allProductsSummary" :key="singleProductSummary">
                                    <td class="border border-slate-300 text-center py-3">{{ singleProductSummary.categoryName }}</td>
                                    <td class="border border-slate-300 text-center py-3">{{ singleProductSummary.categoryQuantity }}</td>
                                    <td class="border border-slate-300 text-center py-3"><a href="/AvailableProduct/">{{ singleProductSummary.totalAvailableQuantity }}</a></td>
                                    <td class="border border-slate-300 text-center py-3"><a href="/TakenProduct/">{{ singleProductSummary.totalTakenQuantity }}</a></td>
                                </tr>
                            </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Unittypes from '../components/unittypes.vue'
import Persons from '../layouts/person.vue'
import TakenProduct from '../components/TakenProduct.vue'
import AvailableProduct from '../components/AvailableProduct.vue'
import AssignItem from '../components/AssignItem.vue'
export default {
    components: {
        Unittypes, Persons, TakenProduct, AvailableProduct, AssignItem
    },
    data() {
        return {
            employeesAssignUnits: [],
            allProductsSummary: [],
            uniqueArray: [],
            eachProduct: [],
            uniqueObject: {}
        }
    },
    mounted () {
        // get localStorage
        this.employeesAssignUnits = JSON.parse(localStorage.getItem('employeeItemMapping')) ? JSON.parse(localStorage.getItem('employeeItemMapping')) : []
        console.log("employeesAssignUnits:", this.employeesAssignUnits);
        this.allProductsSummary = JSON.parse(localStorage.getItem('allProductsCategories')) ? JSON.parse(localStorage.getItem('allProductsCategories')) : []
        console.log("allProductsSummary:", this.allProductsSummary);

        // for(let i = 0; i < this.allProductsSummary.length; i++){
        //         for(let j = 0; j < this.allProductsSummary[i].items.length; j++){
        //             console.log("www:", this.allProductsSummary[i].categoryName);
        //             if(this.allProductsSummary[i].categoryName === this.allProductsSummary[i].items[j].itemCategory){
                        
        //                 console.log("PPP:", this.allProductsSummary[i].items[j].itemCategory);
        //                 let element = this.allProductsSummary[i].items[j].itemBrand
        //             // console.log("XXX", element);
        //             this.eachProduct.push(element)
        //             // console.log("TTTTHHHH:", this.eachProduct);
        //             }
                    
        //         }
        //     }

        // relation with this.allProductsSummary and this.employeeItemMapping
        this.allProductsSummary.forEach((el1, index1) => {
                let reserveCategory = el1.categoryName;
                let totalQuantity = 0;
                let totalTaken = 0;

                this.allProductsSummary[index1].items.filter((el2, index2) => {
                    if(reserveCategory === el2.itemCategory){
                        totalQuantity = totalQuantity + el2.itemQuantity
                    }
                })
                el1.categoryQuantity = totalQuantity
            })

            this.allProductsSummary.forEach((el1, index1) => {
                let reserveCategory = el1.categoryName;
                let allQuantity = el1.categoryQuantity;
                let totalTaken = 0;

                this.employeesAssignUnits.filter((el2, index2) => {
                    if(reserveCategory === el2.itemCategory){
                        totalTaken = totalTaken + el2.itemQuantity
                        // totalQuantity = totalQuantity + el2.itemQuantity
                    }
                })
                el1.totalTakenQuantity = totalTaken
                el1.totalAvailableQuantity = allQuantity - totalTaken
                // el1.categoryQuantity = totalQuantity
            })
        },
    methods: {
        

    },
}
</script>

<style scoped>

</style>