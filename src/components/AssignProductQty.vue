<template>
    <div>
        <div class="w-full">
            <div v-for="(singleBrand, index) in brand" :key="singleBrand" class="flex justify-between items-center my-1"> 
                <p> {{ singleBrand.brand }} </p>
                <div>
                    <button @click="minusButton(index)" class="border border-gray-500 px-3 py-0 me-2 hover:bg-stone-300 ease-in duration-200">
                        -
                    </button>
                        <span>{{ counters[index] }}</span>
                    <button @click="plusButton(index)" class="border border-gray-500 px-3 py-0 ms-2 hover:bg-gray-300 ease-in duration-200">
                        +
                    </button>
                </div>
                <div>
                    <button @click="addAndCloseProductBrand(singleBrand.brand, index)" class="border border-green-700 bg-green-700 hover:bg-green-500 hover:border-green-500 rounded-sm text-white px-2">
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
            console.log("product brands",this.productBrand)
            console.log("BRAAAANNNNNDDDDDD: ", this.brand);
            // this.brand = []
            this.productBrand.forEach(obj => {
                if(this.selectedCategoryName === obj.category) {
                    this.brand.push(obj)
                    console.log('output brand:', obj);
                }
                console.log("selected brands", this.brand)
                });
            
            // this.counters.fill(0, 0, this.brand.length);
            //     console.log("counters op:",this.counters);

            for(let i = 0; i < this.brand.length; i++){
                this.counters.push(0);
            }
                
        },
        methods: {
            minusButton(i) {
                console.log("minus:", this.brand);
                if (this.counters[i] > 0) {
                    this.counters[i] --;
                }
            },
            plusButton(i){
                console.log("plus: ", );
                this.counters[i]++;
            },
            addAndCloseProductBrand(brand, i){
                this.$emit('closeModal')
                this.brand[i].isActive = !this.brand[i].isActive;
                console.log('VALUEEEE:', brand, 'Indexxxxxxxx:', i);
                console.log("All BRANDSSSSSSSSS: ", this.brand);
                let employeeItemMapping = JSON.parse(localStorage.getItem('employeeItemMapping')) ? JSON.parse(localStorage.getItem('employeeItemMapping')) : []
                // TODO: {employee: abc, itemCategory: Mouse, itemBrand: A4tech, itemQuantity: 5}
                const assignedItem = {
                    itemCategory: this.selectedCategoryName,
                    itemBrand: brand,
                    itemQuantity: this.counters[i]
                }
                // TODO: check duplicate and update employeeItemMapping 
                employeeItemMapping.push(assignedItem)
                localStorage.setItem('employeeItemMapping', JSON.stringify(employeeItemMapping))
                this.$emit('employeeItemMappingUpdated')
            },
            addSingleProduct(){
                
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>