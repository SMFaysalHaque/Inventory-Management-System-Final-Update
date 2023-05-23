<template>

    <div class="dashboard-area">
        <div class="grid grid-cols-2 max-xl:grid-cols-1 my-2.5">
            <div class="">
                <p class="text-center border border-slate-200 p-2 bg-red-200">All Units</p>
                <div class="text-center border border-slate-200 p-2">
                    <table class="border-collapse border border-slate-400 w-full">
                        <thead>
                                <tr>
                                    <th class="border border-slate-300 bg-slate-100 w-1/12 py-2 text-center">Status</th>
                                    <th class="border border-slate-300 bg-slate-100 w-2/12 py-2 text-center">Serial</th>
                                    <th class="border border-slate-300 bg-slate-100 w-2/12 py-2 text-center">Type</th>
                                    <th class="border border-slate-300 bg-slate-100 w-3/12 py-2 text-center">Assign To</th>
                                </tr>
                        </thead>
                        <tbody>
                                <tr v-for="(itemEmployee, i) in allUnits" :key="itemEmployee.i">
                                    <td class="border border-slate-300 text-center py-3">Taken</td>
                                    <td class="border border-slate-300 text-center py-3">{{ i + 1 }}</td>
                                    <td class="border border-slate-300 text-center py-3">
                                        <div v-for="(value, key) in itemEmployee.device" :key="value">
                                            {{ key + ":" + value}}
                                        </div>
                                    </td>
                                    <td class="border border-slate-300 text-center py-3">{{ itemEmployee.name }}</td>
                                </tr>
                        </tbody>
                    </table>
                </div>
            </div>
            <div class="">
                <p class="text-center border border-slate-200 p-2 bg-red-200">Product Summary</p>
                <div class="text-center border border-slate-200 p-2">
                    <table class="border-collapse border border-slate-400 w-full">
                            <thead>
                                <tr>
                                    <th class="border border-slate-300 w-80 py-2 bg-slate-100">Product Type</th>
                                    <th class="border border-slate-300 w-80 py-2 bg-slate-100">Total Quantity</th>
                                    <th class="border border-slate-300 w-64 py-2 bg-slate-100">Available</th>
                                    <th class="border border-slate-300 w-64 py-2 bg-slate-100">Taken</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="(singleProduct, i) in allProductTypes" :key="i">
                                    <td class="border border-slate-300 text-center py-3">{{ singleProduct.type }}</td>
                                    <td class="border border-slate-300 text-center py-3">{{ singleProduct.quantity }}</td>
                                    <td class="border border-slate-300 text-center py-3">{{ singleProduct.quantity  - singleProduct.taken}}</td>
                                    <td class="border border-slate-300 text-center py-3">{{ singleProduct.taken }}</td>
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
import Persons from '../components/Employee.vue'
export default {
    components: {
        Unittypes, Persons
    },
    data() {
        return {
            // key: value
            allUnits: [],
            allProductTypes: [],
            // productsName: null,
        }
    },
    mounted () {
        let arr2 = localStorage.getItem('allEmployee')
        this.allUnits = JSON.parse(arr2) ? JSON.parse(arr2) : [];

        let arr = localStorage.getItem('allProductDetails')
        this.allProductTypes = JSON.parse(arr) ? JSON.parse(arr) : [];
        
        // dash board calculation:
        this.allUnits.forEach((el1) => {
            // console.log("All Units in el1:", el1)
            for(let item in el1.device){
                // console.log("Item from el1.device:", item)
                let tempIndex = this.allProductTypes.findIndex((el2) => el2.type === item)
                // console.log("Item from el2", tempIndex)
                if(!Number(this.allProductTypes[tempIndex].taken)){
                    this.allProductTypes[tempIndex].taken = 0
                }
                this.allProductTypes[tempIndex].taken += el1.device[item]
            }
        })
            // this.productNameAmount = JSON.parse(localStorage.getItem('allEmployee'))

            
            

            // this.allProductTypes = JSON.parse(allProductTypes) ? JSON.parse(allProductTypes) : [];
            // console.log(productNameAmount[index].device)
            // for (let i in this.productNameAmount) {
            //     const element = this.productNameAmount[i];
            //     console.log(element) 
            // }
            // this.productsName = Object.keys(itemEmployee.device).map((item) => h('div', itemEmployee.device[item]))
            

        },
    methods: {
        

    },
}
</script>

<style scoped>

</style>