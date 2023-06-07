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
                        <th class="border border-slate-200">Quantity</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td class="border border-slate-200 text-center">xyz</td>
                        <td class="border border-slate-200 text-center">xyz</td>
                        <td class="border border-slate-200 text-center">xyz</td>
                        <td class="border border-slate-200 text-center">xyz</td>
                    </tr>
                    <tr>
                        <td class="border border-slate-200 text-center">xyz</td>
                        <td class="border border-slate-200 text-center">xyz</td>
                        <td class="border border-slate-200 text-center">xyz</td>
                        <td class="border border-slate-200 text-center">xyz</td>
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
            console.log("xxx", this.setNewProduct);
            this.employeeItemMapping = JSON.parse(localStorage.getItem('employeeItemMapping')) ? JSON.parse(localStorage.getItem('employeeItemMapping')) : []
            console.log(this.employeeItemMapping);

            // relation with this.setNewProduct and this.employeeItemMapping
            // let abc = []
            // const myFunction = (item, index) => {
            //     this.availableProduct.push(item.brand)
            // }
            // this.setNewProduct.forEach(myFunction)
            // console.log(this.availableProduct);
            let availableProductQty = this.employeeItemMapping.forEach((item, index) => {
                // console.log("zzzz: ", item.brand);
                console.log("zzzz: ", item);
                for(let i = 0; i < this.setNewProduct.length; i++){
                    
                }
            })
            console.log(availableProductQty);
        },
        methods: {
            name() {
                
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>