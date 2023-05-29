<template>
    <div class="">
        <div class="w-full border border-stone-200 mx-auto p-5">
            <div class="flex justify-between items-center ps-5">
                <p class="font-bold text-lg">Add New Unit</p>
                <button @click="$emit('closeUnitBtn')" class="border border-red-600 bg-red-600 text-white hover:bg-red-500 rounded-sm px-5 py-1">Close</button>
            </div>
            <div class="mx-auto py-5 px-10 space-y-3 w-full">
                <p class="flex flex-nowrap">Category: <input v-model="productCategory.category" class="border rounded-lg contrast-more:border-slate-400 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500 ms-2 w-full" type="text" name="" id=""></p>
                <p class="flex flex-nowrap">Brand: <input v-model="productCategory.brand" class="border rounded-lg contrast-more:border-slate-400 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500 ms-2 w-full" type="text" name="" id=""></p>
                <p class="flex flex-nowrap">Model: <input v-model="productCategory.model" class="border rounded-lg contrast-more:border-slate-400 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500 ms-2 w-full" type="text" name="" id=""></p>
                <p class="flex flex-nowrap">Quantity: <input v-model="productCategory.quantity" class="border rounded-lg contrast-more:border-slate-400 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500 ms-2 w-full" type="text" name="" id=""></p>
                <button @click="addProduct"  class="border border-sky-600 bg-sky-600 text-white hover:bg-sky-500 rounded-sm px-8 py-1">Add New Product</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        emits: ['closeUnitBtn', 'setNewProduct'],
        data() {
            return {
                productCategory: {
                    category: '',
                    brand: '',
                    quantity: 0,
                    Taken: 0,
                    available: 0,
                    employee: {
                        name: '',
                        mobile: '',
                        email: '',
                        id: '',
                        taken: false
                    }
                }
            }
        },
        methods: {
            addProduct() {
                this.$emit('setNewProduct', this.productCategory);
                this.$emit('closeUnitBtn')
                for (let index = 0; index < array.length; index++) {
                    const element = array[index];
                    
                }
            },
            closeModal(){
                this.$emit('closeUnitBtn')
            }
        },
    }
</script>