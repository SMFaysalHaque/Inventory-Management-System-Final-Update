<template>
    <div>
        <div class="flex justify-between items-center my-2.5">
            <p class="font-bold text-lg">Category</p>
            <!-- add Category button start -->
            <button @click="isOpen()" class="border border-green-700 bg-green-700 hover:bg-green-500 hover:border-green-500 rounded-sm text-white px-10 py-2">Add New Category</button>
            <!-- add Category button end -->
        </div>

        <!-- Add New Category button area start -->
        <div v-if="isVisible" class="fixed inset-0 bg-black bg-opacity-60 z-50 w-full h-full flex justify-center items-center">
            <div class="h-auto z-50">
                <div class="w-full border border-stone-200 mx-auto p-5">
                    <div class="flex justify-between items-center ps-5">
                        <p class="font-bold text-lg">Add New Category</p>
                        <button @click="isClosed()" class="border border-red-600 bg-red-600 text-white hover:bg-red-500 rounded-sm px-5 py-1">Close</button>
                    </div>
                    <div class="mx-auto py-5 px-10 space-y-3 w-full">
                        <p class="flex flex-nowrap">Category:
                        <input v-model="productCategory.categoryName" class="border rounded-lg contrast-more:border-slate-400 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500 ms-2 w-full" type="text" name="" id=""></p>
                        <button @click="addCategory(productCategory.categoryName, i)" class="border border-sky-600 bg-sky-600 text-white hover:bg-sky-500 rounded-sm px-8 py-1">Add Category</button>
                    </div>
                </div>
            </div>
        </div>
        <!-- Add New Category button area end -->

        <!-- category and it's details start -->
        <div class="flex bg-gray-100 font-sans rounded-md my-2">

            <!-- sidebar start -->
            <div class="sidebar top-0 bottom-0 lg:left-0 left-[-300px] w-[400px] overflow-y-auto text-start bg-gray-300 shadow h-screen rounded-s-md">
                <p class="ps-4 py-2 font-semibold">Category Information</p>
                <div @click="isOpenCategoryDetails(item.categoryName, i)" v-for="(item, i) in allProductsCategories" :key="item" class="flex ps-3 py-2 w-full hover:bg-slate-100 hover:ease-in duration-150 border-y">
                    <p class="px-2">{{ i + 1 }}</p>
                    <div class="me-20 px-2">
                        <p>{{ item.categoryName }}</p>
                    </div>
                    <button @click="isOpenBrand()" class="border border-green-700 bg-green-700 hover:bg-green-500 hover:border-green-500 rounded-sm text-white px-2">add</button>
                </div>
            </div>
            <!-- sidebar end -->

            <!-- add category brand info area start  -->
            <div v-if="isVisibleBrand" class="fixed inset-0 bg-black bg-opacity-60 z-50 w-full h-full flex justify-center items-center">
                <div class="h-auto z-50">
                    <div class="w-full border border-stone-200 mx-auto p-5">
                        <div class="flex justify-between items-center ps-5">
                            <p class="font-bold text-lg">Add New Brand</p>
                            <button @click="isClosedBrand()" class="border border-red-600 bg-red-600 text-white hover:bg-red-500 rounded-sm px-5 py-1">Close</button>
                        </div>
                        <div v-for="(item, i) in productCategory.items" :key="item" class="mx-auto py-5 px-10 space-y-3 w-full">
                            <p class="flex flex-nowrap">Brand:
                            <input v-model="item.itemBrand" class="border rounded-lg contrast-more:border-slate-400 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500 ms-2 w-full" type="text" name="" id=""></p>
                            <p class="flex flex-nowrap">Model:
                            <input v-model="item.itemModel" class="border rounded-lg contrast-more:border-slate-400 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500 ms-2 w-full" type="text" name="" id=""></p>
                            <p class="flex flex-nowrap">Quantity:
                            <input v-model="item.itemQuantity" class="border rounded-lg contrast-more:border-slate-400 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500 ms-2 w-full" type="text" name="" id=""></p>
                            <button @click="addBrand(item.itemBrand)" class="border border-sky-600 bg-sky-600 text-white hover:bg-sky-500 rounded-sm px-8 py-1">Add Brand</button>
                        </div>
                    </div>
                </div>
            </div>
            <!-- add category brand info area end  -->

            <!-- product unit info start -->
            <div v-if="isVisibleCategoryDetails" class="w-full">
                    <p class="ps-5 py-2 font-semibold border-y border-gray-300 rounded-tr-md">{{ allProductsCategories.categoryName }}</p>
                <table class="table-auto w-[95%] ms-5 mt-5 border-collapse border border-slate-300">
                    <thead>
                        <tr class="h-10 bg-gray-300 border-b-2 border-gray-400">
                            <th class="border border-slate-200">Brand</th>
                            <th class="border border-slate-200">Model</th>
                            <th class="border border-slate-200">Quantity</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td class="border border-slate-200 text-center">Brand</td>
                            <td class="border border-slate-200 text-center">Model</td>
                            <td class="border border-slate-200 text-center">Quantity</td>
                        </tr>
                    </tbody>
                </table>
                
                <!-- assign unit button start -->
                <button class="border border-sky-300 rounded-sm contrast-more:border-sky-100 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500 hover:bg-sky-500 hover:text-white px-10 py-1 ms-5 mt-5 ease-in duration-200">Assign Units</button>
                <!-- assign unit button end -->

                <!-- assignItem unit area start -->
                <!-- <div>
                    <AssignItem />
                </div> -->
                <!-- assignItem unit area end -->
            </div>
            <!-- product unit info end -->
        </div>
        <!-- category and it's details end -->
    </div>
</template>

<script>
    export default {
        data() {
            return {
                isVisibleCategoryDetails: false,
                isVisible: false,
                isVisibleBrand: false,
                allProductsCategories: [],
                singleProductCategory: [], //for deep clone
                x: [],
                brandInfo: [],
                productCategory: {
                    categoryName: '',
                    categoryQuantity: 0,
                    items: [
                        {
                        itemBrand: '',
                        itemModel: '',
                        itemQuantity: 0
                    }
                    ]
                },
                // selectedProductCategory: {

                // }
            }
        },
        mounted () {
            // get localStorage
            this.allProductsCategories = JSON.parse(localStorage.getItem('allProductsCategories')) ? JSON.parse(localStorage.getItem('allProductsCategories')) : []
            console.log("SINGLE PRODUCT CATEGORY LIST: ", this.allProductsCategories);
        },
        methods: {
            isOpen() {
                this.isVisible = true
            },
            isOpenCategoryDetails(value, i){
                this.isVisibleCategoryDetails = true
                this.allProductsCategories.categoryName = value
            },
            isOpenBrand(){
                this.isVisibleBrand = true
            },
            isClosed() {
                this.isVisible = false
            },
            isClosedBrand(){
                this.isVisibleBrand = false
            },
            addCategory(value, i){
                console.log(value);
                this.isVisible = false
                this.singleProductCategory = JSON.parse(JSON.stringify(this.productCategory)) //deep clone
                console.log("All SINGLE product category:", this.singleProductCategory);
                this.allProductsCategories.push(this.singleProductCategory)
                console.log("All product category:", this.allProductsCategories);
                
                this.productCategory.categoryName = ""; // empty modal category name.

                // set localStorage
                localStorage.setItem('allProductsCategories', JSON.stringify(this.allProductsCategories))
            },
            addBrand(value){
                console.log(value);
                this.isVisibleBrand = false
                this.brandInfo = this.productCategory.items
                console.log("Brand Info:", this.brandInfo);
                this.x.push(this.brandInfo)
                console.log("Print X:", this.x);
            },
        },
    }
</script>

<style lang="scss" scoped>

</style>