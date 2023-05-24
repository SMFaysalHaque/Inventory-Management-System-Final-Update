<template>
    <div class="">
        <div class="flex items-center justify-between my-2.5">
            <p class="font-bold text-lg">Unit Types</p>
            <button class="border border-green-700 bg-green-700 hover:bg-green-500 hover:border-green-500 rounded-sm text-white px-10 py-2">Add New Unit</button>
        </div>

        <!-- addnewunit emit start here -->
        <div class="py-2">
            <Addnewunit />
        </div>
        <!-- addnewunit emit end here -->
        
        <!-- <div class="grid grid-cols-6 bg-slate-100 border border-cyan-700">
            <div class="col-span-2 flex justify-center items-center p-2">
                <p>Category</p>
            </div>
            <div class="col-span-4 flex justify-center items-center border p-2">
                <p>Details</p>
            </div>
        </div>
        <div class="grid grid-cols-6 border border-cyan-700">
            <div class="col-span-2 flex justify-center items-center border-e-2">
                <p>Category Name:</p>
            </div>
            <div class="col-span-4 flex flex-col justify-center ps-10 py-10 space-y-3">
                <p>Brand:</p>
                <p>Model:</p>
                <p>Quantity:</p>
            </div>
        </div> -->

        <!-- New product added table start -->
        <div class="w-full bg-gray-100 h-screen my-5 rounded-md">
            <p class="font-bold text-md ms-5 pt-5">All Products</p>
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
        <!-- New product added table end -->
    </div>
</template>


<script>
import Addnewunit from '../components/addnewunit.vue';
    export default {
        components: {
            Addnewunit,
        },
        data() {
            return {
            }
        },
        mounted () {
        },
        methods: {
            showModal() {
            },
            closeModal() {
            },
            getProductData(value){
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>