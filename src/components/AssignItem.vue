<template>
    <div>
        <div class="assign-area border border-stone-300 rounded-md w-full my-5 px-1 py-1">
            <p class="flex w-auto"><input class="border rounded-lg contrast-more:border-slate-400 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500 px-1 me-1 w-full" type="search" name="" id="" placeholder="Search"><button class="border border-red-600 bg-red-600 text-white hover:bg-red-500 rounded-sm px-2" @click="closeModal(i)">Close</button></p>
            <p v-for="(assignProduct, i) in products" :key="assignProduct.i" class="flex justify-between items-center py-1">{{ assignProduct.type }}<button class="border border-green-700 bg-green-700 hover:bg-green-500 hover:border-green-500 rounded-sm text-white px-2" @click="assignItem(assignProduct.type)">add</button></p>
        </div>
    </div>
</template>

<script>
    export default {
        emits: ['close', 'assignProduct'],
        data() {
            return {
                // key: value
                products: []
            }
        },
        mounted () {
            this.products = JSON.parse(localStorage.getItem('allProductDetails'))
        },
        methods: {
            assignItem(type) {
                this.$emit('assignProduct', type)
                console.log('aaa', type)
            },
            closeModal(){
                this.$emit('close')
            },
            
        },
    }
</script>

<style lang="scss" scoped>

</style>