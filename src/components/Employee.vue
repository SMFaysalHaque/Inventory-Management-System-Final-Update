<template>
    <div>
        <div class="flex items-center justify-between my-2.5">
            <p class="font-bold text-lg">Employee List</p>
            <button @click="isShowed()" class="border border-green-700 bg-green-700 hover:bg-green-500 hover:border-green-500 rounded-sm text-white px-10 py-2">Add New Employee</button>
        </div>
        <!-- -->
        <div class="py-2" v-if="isModalVisible">
            <Addnewemployee @addNewEmployee="getEmployeeData" @close="isClosed()" />
        </div>
        <!--  -->
        <table class="table-auto border-collapse border border-slate-400 w-full">
            <thead>
                <tr>
                    <th class="border border-slate-300 ...">S. No.</th>
                    <th class="border border-slate-300 ...">Employee Name</th>
                    <th class="border border-slate-300 ...">Mobile</th>
                    <th class="border border-slate-300 ...">E-mail</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(employee, i) in allEmployee" :key="employee.id">
                    <td class="border border-slate-300 text-center">{{ i+1 }}</td>
                    <td class="border border-slate-300 text-center">{{ employee.name }}</td>
                    <td class="border border-slate-300 text-center">{{ employee.mobile }}</td>
                    <td class="border border-slate-300 text-center">{{ employee.email }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
import Addnewemployee from '../components/Addnewemployee.vue'
import { employee } from '../Store/store.js'
    export default {
        components: {
            Addnewemployee
        },
        data() {
            return {
                allEmployee: [],
                isModalVisible: false
            }
        },
        mounted(){
            this.allEmployee = JSON.parse(localStorage.getItem('allEmployee')) ? JSON.parse(localStorage.getItem('allEmployee')) : []
            // console.log(this.allEmployee[3].devices)
        },
        methods: {
            isShowed() {
                this.isModalVisible = true;
                console.log('aaa')
            },
            isClosed() {
                this.isModalVisible = false;
            },
            getEmployeeData(value){
                this.allEmployee.push(value);
                localStorage.setItem('allEmployee', JSON.stringify(this.allEmployee))
                // allEmployeeData.set(this.allEmployee)
                // console.log(allEmployeeData.get())
            },
        }
    }
</script>

<style lang="scss" scoped>

</style>