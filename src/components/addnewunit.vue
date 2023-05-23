<template>
    <div class="">
        <div class="w-5/12 border border-stone-200 mx-auto p-5">
            <div class="flex justify-between items-center ps-5">
                <p class="font-bold text-lg">Add New Unit</p>
                <button @click="$emit('close')" class="border border-red-600 bg-red-600 text-white hover:bg-red-500 rounded-sm px-5 py-2">Close</button>
            </div>
            <div class="mx-auto py-5 px-10 space-y-3">
                <p>Type: <input v-model="info.type" class="border rounded-lg contrast-more:border-slate-400 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500 ms-1" type="text" name="" id=""></p>
                <p>Model: <input v-model="info.model" class="border rounded-lg contrast-more:border-slate-400 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500 ms-1" type="text" name="" id=""></p>
                <p>Quantity: <input v-model="info.quantity" class="border rounded-lg contrast-more:border-slate-400 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500 ms-1 w-56" type="text" name="" id=""></p>
                <button @click="addProducet()" class="border border-sky-600 bg-sky-600 text-white hover:bg-sky-500 rounded-sm px-8 py-1">Add New Product</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        emits: ['close', 'addNewProduct'],
        data() {
            return {
                info: {
                    type: '',
                    model: '',
                    quantity: '',
                    status: 'available',
                    status: 'taken',
                    taken: ''
                }
            }
        },
        methods: {
            addProducet() {
                this.$emit('addNewProduct', this.info);
                this.$emit('close')
            }
        },
    }
</script>