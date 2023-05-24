<template>

    <div class="dashboard-area">
        <div class="grid grid-cols-2 max-xl:grid-cols-1 w-full bg-gray-100 h-screen p-5 rounded-md my-2.5">
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
                                    <th class="border border-slate-300 bg-blue-100 w-3/12 py-2 text-center">Assign To</th>
                                </tr>
                        </thead>
                        <tbody>
                                <tr>
                                    <td class="border border-slate-300 text-center py-3">Taken</td>
                                    <td class="border border-slate-300 text-center py-3">01</td>
                                    <td class="border border-slate-300 text-center py-3">
                                        <!-- <div v-for="(value, key) in itemEmployee.device" :key="value">
                                            {{ key + ":" + value}}
                                        </div> -->
                                        Mouse
                                    </td>
                                    <td class="border border-slate-300 text-center py-3">A4tech</td>
                                    <td class="border border-slate-300 text-center py-3">Faysal</td>
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
                                <tr>
                                    <td class="border border-slate-300 text-center py-3">Mouse</td>
                                    <td class="border border-slate-300 text-center py-3">10</td>
                                    <td class="border border-slate-300 text-center py-3"><a href="/AvailableProduct/">3</a></td>
                                    <td class="border border-slate-300 text-center py-3"><a href="/TakenProduct/">7</a></td>
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
        }
    },
    mounted () {
        },
    methods: {
        

    },
}
</script>

<style scoped>

</style>