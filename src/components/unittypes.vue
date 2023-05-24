<template>
    <div class="">
        <div class="flex items-center justify-between my-2.5">
            <p class="font-bold text-lg">Unit Types</p>
            <button @click="isShowed()" class="border border-green-700 bg-green-700 hover:bg-green-500 hover:border-green-500 rounded-sm text-white px-10 py-2">Add New Unit</button>
        </div>

        <!-- addnewunit emit start here -->
        <div class="py-2" v-if="isVisible">
            <Addnewunit @click="isClosed()"/>
        </div>
        <!-- addnewunit emit end here -->

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
                isVisible: false
            }
        },
        mounted () {
        },
        methods: {
            isShowed() {
                this.isVisible = true
            },
            isClosed() {
                this.isVisible = false
            },
            getProductData(value){
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>