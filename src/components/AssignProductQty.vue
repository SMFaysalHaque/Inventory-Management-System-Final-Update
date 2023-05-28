<template>
    <div>
        <div class="w-full">
            <div v-for="(singleBrand, i) in productBrand" :key="singleBrand.i" class="flex justify-between items-center"> {{ singleBrand.brand }} 
                <p>
                    <button @click="minusButton()" class="border border-gray-500 px-3 py-0 me-2 hover:bg-stone-300 ease-in duration-200">
                        -
                    </button> 
                        <span>{{ counter }}</span>
                    <button @click="plusButton()" class="border border-gray-500 px-3 py-0 ms-2 hover:bg-gray-300 ease-in duration-200">
                        +
                    </button>
                </p>
                <button class="border border-green-700 bg-green-700 hover:bg-green-500 hover:border-green-500 rounded-sm text-white px-2">
                    add
                </button>
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
        data() {
            return {
                counter: 0,
                productBrand: []
            }
        },
        mounted () {
            this.productBrand = JSON.parse(localStorage.getItem('setNewProduct')) ? JSON.parse(localStorage.getItem('setNewProduct')) : [];
        },
        methods: {
            minusButton() {
                if(this.counter <= 0){
                    return this.counter
                }
                else{
                    return this.counter--
                }
            },
            plusButton(){
                this.counter++
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>