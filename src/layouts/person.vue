<template>
    <div>
        <div class="flex justify-between items-center my-2.5">
            <p class="font-bold text-lg">Persons</p>
            <!-- add employee button start -->
            <button @click="isShowedEmployeeModal()" class="border border-green-700 bg-green-700 hover:bg-green-500 hover:border-green-500 rounded-sm text-white px-10 py-2">Add New Employee</button>
            <!-- add employee button end -->
        </div>

        <!-- Add New Employee button area start -->
        <div v-if="isVisibleEmployeeModal" class="fixed inset-0 bg-black bg-opacity-60 z-50 w-full h-full flex justify-center items-center">
            <div class="h-auto z-50">
                <Addnewemployee @close="isClosedEmployeeModal" class="flex relative bg-stone-200"/>
            </div>
        </div>
        <!-- Add New Employee button area end -->

        <!-- employee info and their products unit start -->
        <div class="flex bg-gray-100 font-sans rounded-md my-2">

            <!-- sidebar start -->
            <div class="sidebar top-0 bottom-0 lg:left-0 left-[-300px] w-[300px] overflow-y-auto text-start bg-gray-300 shadow h-screen rounded-s-md">
                <p class="ps-4 py-2 font-semibold">Employee Information</p>
                <div class="flex ps-3 py-2 w-full hover:bg-slate-100 hover:ease-in duration-150 border-y">
                    <p class="px-2">01</p>
                    <div class="px-2">
                        <p>S. M. Faysal Haque</p>
                        <p>faysal@gmail.com</p>
                        <p>Mobile: 0172-2222222</p>
                        <p>ID: 0001-04-2023</p>
                    </div>
                </div>
                <div class="flex ps-3 py-2 w-full hover:bg-slate-100 hover:ease-in duration-150 border-y">
                    <p class="px-2">02</p>
                    <div class="px-2">
                        <p>Nayeem Hossain</p>
                        <p>nayeem@gmail.com</p>
                        <p>Mobile: 0156-6666666</p>
                        <p>ID: 0002-12-2021</p>
                    </div>
                </div>
            </div>
            <!-- sidebar end -->

            <!-- product unit info start -->
            <div class="w-full">
                <p class="ps-5 py-2 font-semibold border-y border-gray-300 rounded-tr-md">S. M. Faysal Haque</p>
                <p class="ms-5 pt-4 text-gray-500">E-mail <span class="ps-2 text-sky-500">faysal@gmail.com</span></p>
                <p class="ms-5 pt-1 text-gray-500">Mobile <span class="ps-2 text-sky-500">0172-2222222</span></p>
                <table class="table-auto w-[95%] ms-5 mt-5 border-collapse border border-slate-300">
                    <thead>
                        <tr class="h-10 bg-gray-300 border-b-2 border-gray-400">
                            <th class="border border-slate-200 w-[35%]">Category</th>
                            <th class="border border-slate-200">Brand</th>
                            <th class="border border-slate-200">Model</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td class="border border-slate-200 text-center">xyz</td>
                            <td class="border border-slate-200 text-center">xyz</td>
                            <td class="border border-slate-200 text-center">xyz</td>
                        </tr>
                        <tr>
                            <td class="border border-slate-200 text-center">xyz</td>
                            <td class="border border-slate-200 text-center">xyz</td>
                            <td class="border border-slate-200 text-center">xyz</td>
                        </tr>
                    </tbody>
                </table>
                
                <!-- assign unit button start -->
                <button @click="isShowedUnitAddModal()" class="border border-sky-300 rounded-sm contrast-more:border-sky-100 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500 hover:bg-sky-500 hover:text-white px-10 py-1 ms-5 mt-5 ease-in duration-200">Assign Units</button>
                <!-- assign unit button end -->

                <!-- assignItem unit area start -->
                <div v-if="isVisibleUnitAddModal">
                    <AssignItem  @closeAssignBtn="isClosedUnitAddModal"/>
                </div>
                <!-- assignItem unit area end -->
            </div>
            <!-- product unit info end -->
        </div>
        <!-- employee info and their products unit end -->
    </div>
</template>

<script>
import Addnewemployee from '../components/Addnewemployee.vue'
import AssignItem from '../components/AssignItem.vue'
    export default {
        components: {
            AssignItem, Addnewemployee
        },
        data() {
            return {
                isVisibleEmployeeModal: false,
                isVisibleUnitAddModal: false
            }
        },
        mounted(){
        },
        methods: {
            // show modals
            isShowedEmployeeModal(){
                this.isVisibleEmployeeModal = true
            },
            isShowedUnitAddModal(){
                this.isVisibleUnitAddModal = true
            },

            // close modals
            isClosedEmployeeModal(){
                this.isVisibleEmployeeModal = false
            },
            isClosedUnitAddModal(){
                this.isVisibleUnitAddModal = false
            },
            assignProduct(){
            }
        }
    }
</script>