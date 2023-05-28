<template>
    <div>
        <div class="w-full border border-stone-200 mx-auto p-5">
            <div class="flex justify-between items-center ps-5">
                <p class="font-bold text-lg">Add Employee</p>
                <button @click="$emit('close')" class="border border-red-600 bg-red-600 text-white hover:bg-red-500 rounded-sm px-5 py-1">Close</button>
            </div>
            <div class="mx-auto py-5 px-10 space-y-3">
                <p class="flex flex-nowrap">Name: <input v-model="employeeInfo.name" class="border rounded-lg contrast-more:border-slate-400 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500 ms-2 w-full" type="text" name="" id=""></p>
                <p class="flex flex-nowrap">Email: <input v-model="employeeInfo.email" class="border rounded-lg contrast-more:border-slate-400 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500 ms-2 w-full" type="text" name="" id=""></p>
                <p class="flex flex-nowrap">Mobile: <input v-model="employeeInfo.mobile" class="border rounded-lg contrast-more:border-slate-400 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500 ms-2 w-full" type="text" name="" id=""></p>
                <p class="flex flex-nowrap">Id: <input v-model="employeeInfo.id" class="border rounded-lg contrast-more:border-slate-400 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500 ms-2 w-full" type="text" name="" id=""></p>
                <button @click="addNewEmployee" class="border border-sky-600 bg-sky-600 text-white hover:bg-sky-500 rounded-sm px-8 py-1">Add New Employee</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        emits: ['close', 'addNewEmployee'],
        data() {
            return {
                employeeInfo: {
                    name: '',
                    mobile: '',
                    email: '',
                    id: '',
                    taken: false,
                    Products: [
                        {
                            category: '',
                            brand: '',
                            quantity: 0
                        }
                    ]
                },
            }
        },
        mounted () {
            ;
        },
        methods: {
            addNewEmployee() {
                this.$emit('addNewEmployee', this.employeeInfo)
                this.$emit('close')
            },
            closeModal(){
                this.$emit('close')
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>