<template>
    <div>
        <div class="assign-area border border-stone-300 rounded-sm w-[500px] ms-5 mt-3 px-1 py-1">
            <p class="flex w-auto"><input class="border rounded-lg contrast-more:border-slate-400 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500 px-1 me-1 w-full" type="search" name="" id="" placeholder="Search"><button class="border border-red-600 bg-red-600 text-white hover:bg-red-500 rounded-sm px-2" @click="$emit('closeAssignBtn')">Close</button></p>
            <p class="flex justify-between items-center py-1">Mouse<button @click="brandProductModal()" class="border border-green-700 bg-green-700 hover:bg-green-500 hover:border-green-500 rounded-sm text-white px-2">add</button></p>
            <div v-if="isBrandProductVisible">
                <AssignProductQty />
            </div>
        </div>
    </div>
</template>

<script>
import AssignProductQty from './AssignProductQty.vue'
    export default {
        emits: ['closeAssignBtn', ''],
        components: {
            AssignProductQty
        },
        data() {
            return {
                // key: value
                products: [],
                isBrandProductVisible: false
            }
        },
        mounted () {
        },
        methods: {
            assignItem() {
            },
            closeModal(){
                this.$emit('closeAssignBtn')
            },
            brandProductModal(){
                this.isBrandProductVisible = true
            }
            
        },
    }
</script>

<style lang="scss" scoped>

</style>