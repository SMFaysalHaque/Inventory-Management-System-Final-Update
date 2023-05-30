<template>
    <div>
        <div class="w-full">
            <div v-for="(singleBrand, index) in brand" :key="singleBrand" class="flex justify-between items-center"> {{ singleBrand.brand }} 
                <div v-for="(counter, i) in counters" :key="counter">
                    <button @click="minusButton($event, i)" class="border border-gray-500 px-3 py-0 me-2 hover:bg-stone-300 ease-in duration-200">
                        -
                    </button> 
                        <span>{{ counters }}</span>
                    <button @click="plusButton($event, i)" class="border border-gray-500 px-3 py-0 ms-2 hover:bg-gray-300 ease-in duration-200">
                        +
                    </button>
                </div>
                <div>
                    <button @click="closeProductBrand(i)" class="border border-green-700 bg-green-700 hover:bg-green-500 hover:border-green-500 rounded-sm text-white px-2">
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
        props:{
            selectedItemName : {
                type: String,
                default: null
            }
        },
        data() {
            return {
                counters: [0],
                productBrand: [],
                brand: [],
                isVisibleProductBrand: false,
            }
        },
        mounted () {
            this.productBrand = JSON.parse(localStorage.getItem('setNewProduct')) ? JSON.parse(localStorage.getItem('setNewProduct')) : [];
            console.log("product brands",this.productBrand)
            this.brand = []
            this.productBrand.forEach(obj => {
                if(this.selectedItemName === obj.category) {
                    this.brand.push(obj)
                }
                console.log("selected brands", this.brand)
                });
                
                
        },
        methods: {
            minusButton(type, i) {
                console.log("++++", type);
                if (this.counters[i] > 0) {
                    this.counters[i] --;
                }
            },
            plusButton(type, i){
                console.log("----", type);
                this.counters[i]++;
            },
            closeProductBrand(i){
                this.isVisibleProductBrand = true
                console.log('Close tab', i);
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>