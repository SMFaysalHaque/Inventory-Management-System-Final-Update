<template>
    <div>
        <div class="w-full">
            <div v-for="(singleBrand, index) in brand" :key="singleBrand" class="flex justify-between items-center my-1"> 
                <p> {{ singleBrand.brand }} </p>
                <p>{{ singleBrand.model }}</p>
                <div>
                    <button @click="minusButton(index)" class="border border-gray-500 px-3 py-0 me-2 hover:bg-stone-300 ease-in duration-200">
                        -
                    </button>
                        <span>{{ counters[index] }}</span>
                    <button @click="plusButton(singleBrand.quantity, index)" class="border border-gray-500 px-3 py-0 ms-2 hover:bg-gray-300 ease-in duration-200">
                        +
                    </button>
                </div>
                <div>
                    <button @click="addAndCloseProductBrand(singleBrand.brand, singleBrand.model, index)" class="border border-green-700 bg-green-700 hover:bg-green-500 hover:border-green-500 rounded-sm text-white px-2">
                    add
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Unittypes from '../components/unittypes.vue'
    export default {
        components: {
            Unittypes
        },
        emits: ['close', 'closeModal', 'employeeItemMappingUpdated'],
        props:{
            selectedCategoryName : {
                type: String,
                default: null
            },
            closeCategory : {
                type: Boolean,
                default: false
            },
            selectedEmployee : {
                type: Object,
                default: null
            }
        },
        data() {
            return {
                counters: [],
                productBrand: [],
                brand: [],
                isVisibleProductBrand: false,
            }
        },
        mounted () {
            this.productBrand = JSON.parse(localStorage.getItem('setNewProduct'));
            console.log("PRODUCT BRAND:", this.productBrand);
            console.log("BRAND:", this.brand);
            this.productBrand.forEach(obj => {
                if(this.selectedCategoryName === obj.category) {
                    this.brand.push(obj)
                }
                });

            for(let i = 0; i < this.brand.length; i++){
                this.counters.push(0);
            }
                
        },
        methods: {
            minusButton(i) {
                if (this.counters[i] > 0) {
                    this.counters[i] --;
                }
            },
            plusButton(value, i){
                if(this.counters[i] < value){
                    this.counters[i]++
                }
                
            },
            addAndCloseProductBrand(brand, model, i){
                this.$emit('closeModal')
                this.brand[i].isActive = !this.brand[i].isActive;
                
                //parse assignedItem:
                let employeeItemMapping = JSON.parse(localStorage.getItem('employeeItemMapping')) ? JSON.parse(localStorage.getItem('employeeItemMapping')) : []

                if (this.selectedEmployee === null){
                    console.log("No selected employee.");
                    return
                }
                const assignedItem = {
                    employeeName: this.selectedEmployee.name,
                    employeeEmail: this.selectedEmployee.email,
                    itemCategory: this.selectedCategoryName,
                    itemBrand: brand,
                    itemModel: model,
                    itemQuantity: this.counters[i]
                } 
                employeeItemMapping.push(assignedItem)
                localStorage.setItem('employeeItemMapping', JSON.stringify(employeeItemMapping))
                this.$emit('employeeItemMappingUpdated')
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>