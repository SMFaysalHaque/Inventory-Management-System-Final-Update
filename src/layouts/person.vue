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
                <Addnewemployee @addNewEmployee="setEmployeeInfo" @close="isClosedEmployeeModal" class="flex relative bg-stone-200"/>
            </div>
        </div>
        <!-- Add New Employee button area end -->

        <!-- employee info and their products unit start -->
        <div class="flex bg-gray-100 font-sans rounded-md my-2">

            <!-- sidebar start -->
            <div class="sidebar top-0 bottom-0 lg:left-0 left-[-300px] w-[300px] overflow-y-auto text-start bg-gray-300 shadow h-screen rounded-s-md">
                <p class="ps-4 py-2 font-semibold">Employee Information</p>
                <div @click="isShowedEmployeeAllUnits(employee, i)" v-for="(employee, i) in allEmployeeList" :key="employee.i" class="flex ps-3 py-2 w-full hover:bg-slate-100 hover:ease-in duration-150 border-y">
                    <p class="px-2">{{ i + 1 }}</p>
                    <div class="px-2">
                        <p>{{ employee.name }}</p>
                        <p>{{ employee.email }}</p>
                        <p>Mobile: {{ employee.mobile }}</p>
                        <p>ID: {{ employee.id }}</p>
                    </div>
                </div>
            </div>
            <!-- sidebar end -->

            <!-- product unit info start -->
            <div v-if="isVisibleEmployeeAllUnits" class="w-full">
                <!-- <div v-for="(singleEmployee, i) in selectedEmployee" :key="singleEmployee.i"> -->
                    <p class="ps-5 py-2 font-semibold border-y border-gray-300 rounded-tr-md">{{ selectedEmployee.name }}</p>
                    <p class="ms-5 pt-4 text-gray-500">E-mail <span class="ps-2 text-sky-500">{{ selectedEmployee.email }}</span></p>
                    <p class="ms-5 pt-1 text-gray-500">Mobile <span class="ps-2 text-sky-500">{{ selectedEmployee.mobile }}</span></p>
                <!-- </div> -->
                <table class="table-auto w-[95%] ms-5 mt-5 border-collapse border border-slate-300">
                    <thead>
                        <tr class="h-10 bg-gray-300 border-b-2 border-gray-400">
                            <th class="border border-slate-200 w-[35%]">Category</th>
                            <th class="border border-slate-200">Brand</th>
                            <th class="border border-slate-200">Quantity</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="item in employeeItemMapping" :key="item">
                            <td class="border border-slate-200 text-center">{{ item.itemCategory }}</td>
                            <td class="border border-slate-200 text-center">{{ item.itemBrand }}</td>
                            <td class="border border-slate-200 text-center">{{ item.itemQuantity }}</td>
                        </tr>
                    </tbody>
                </table>
                
                <!-- assign unit button start -->
                <button @click="isShowedUnitAddModal()" class="border border-sky-300 rounded-sm contrast-more:border-sky-100 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500 hover:bg-sky-500 hover:text-white px-10 py-1 ms-5 mt-5 ease-in duration-200">Assign Units</button>
                <!-- assign unit button end -->

                <!-- assignItem unit area start -->
                <div v-if="isVisibleUnitAddModal">
                    <AssignItem @employeeItemMappingUpdated="getEmployeeItemMapping()" @closeModal="isClosedUnitAddModal(i)" @closeAssignBtn="isClosedUnitAddModal"/>
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
                isVisibleEmployeeAllUnits: false,
                isVisibleEmployeeModal: false,
                isVisibleUnitAddModal: false,
                allEmployeeList: [],
                employeeItemMapping: [],
                selectedEmployee: {
                    name: '',
                    mobile: '',
                    email: '',
                    id: '',
                    taken: false,
                    products: [
                        {
                            category: '',
                            brand: '',
                            quantity: 0
                        }
                    ]
                }
            }
        },
        mounted(){
            this.allEmployeeList = JSON.parse(localStorage.getItem('allEmployeeList')) ? JSON.parse(localStorage.getItem('allEmployeeList')) : []
            console.log("ALL EMPLOYEE LIST: ", this.allEmployeeList);

            this.selectedEmployee.products = JSON.parse(localStorage.getItem('setNewProduct'))
            console.log("JSON DATA:", this.selectedEmployee.products);
            this.getEmployeeItemMapping()
            // console.log("aaaaa", this.selectedEmployee.products);
            // console.log("MMMMMM: ", this.employeeAssignProduct);

            //get type quantity                                                 
            // const allProducts = localStorage.getItem('setNewProduct')
            // let brandQuantity = 0
            // for (let index = 0; index < allProducts.length; index++) {
            //     const product = allProducts[index];
            //     if (product.brand === brand) {
            //         brandQuantity = product.quantity
            //     }
            // }
            // // count number of taken units
            // let takenUnits = 0
            // for (let index = 0; index < this.personInfos.length; index++) {
            //     const person = this.personInfos[index];
            //     takenUnits = takenUnits + person.device[type]
            // }
            // // if product available assign it to person else give alert
            // if (takenUnits <= typeQuantity){
            
            //     const currentPerson = this.personInfos[index]
            //     if(!currentPerson.device[type]){
            //         currentPerson.device[type] = 1;
            //     }
            //     else{
            //         currentPerson.device[type] = currentPerson.device[type] + 1
            //     }
            //     console.log("currentPerson", currentPerson);
            //     localStorage.setItem('allEmployee', JSON.stringify(this.personInfos))
            // }
            // else{
            //     alert(`${type} is not available`)
            // }
        },
        methods: {
            // show all units area
            isShowedEmployeeAllUnits(value, i){
                this.isVisibleEmployeeAllUnits = true
                this.selectedEmployee = value
                console.log(this.selectedEmployee);
                
            },
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
            isClosedUnitAddModal(i){
                this.isVisibleUnitAddModal = false
            },

            // set employee list
            setEmployeeInfo(value){
                this.allEmployeeList.push(value)
                localStorage.setItem('allEmployeeList', JSON.stringify(this.allEmployeeList))
            },
            getEmployeeItemMapping(){
                this.employeeItemMapping = JSON.parse(localStorage.getItem('employeeItemMapping')) ? JSON.parse(localStorage.getItem('employeeItemMapping')) : []
            }
        }
    }
</script>