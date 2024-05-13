<template>
    <div>
        <div
            class="assign-area border border-stone-300 rounded-sm w-[500px] ms-5 mt-3 px-1 py-1"
        >
            <div
                class="flex justify-between items-center border-b-2 w-auto pb-1"
            >
                <p class="font-bold">
                    Assign Units
                    <input
                        class="border rounded-lg contrast-more:border-slate-400 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500 px-1 me-1 w-full hidden"
                        type="search"
                        name=""
                        id=""
                        placeholder="Search"
                    />
                </p>
                <button
                    class="border border-red-600 bg-red-600 text-white hover:bg-red-500 rounded-sm px-2"
                    @click="$emit('closeAssignBtn')"
                >
                    Close
                </button>
            </div>
            <div
                v-for="(singleProduct, i) in filterProduct"
                :key="i"
                class=""
            >
                <div class="flex justify-between items-center py-1">
                    <p>{{ singleProduct.categoryName }}</p>
                    <button
                        @click="
                            brandProductModal(singleProduct.categoryName, i)
                        "
                        class="border border-green-700 bg-green-700 hover:bg-green-500 hover:border-green-500 rounded-sm text-white px-2 me-1"
                        :class="{'hidden' : selectedIndex == i, 'pointer-events-none opacity-50' : selectedIndex !== -1}"
                        :disabled="selectedIndex !== -1"
                    >
                        add
                    </button>
                    <button
                        class="border border-red-600 bg-red-600 hover:bg-red-500 w-5 h-5 rounded-full ps-[1px]"
                        :class="selectedIndex != i ? 'hidden' : 'block'"
                        @click="closeItem(i)"
                    >
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none">
                        <path d="M4.70703 3.29297L3.29297 4.70703L10.5859 12L3.29297 19.293L4.70703 20.707L12 13.4141L19.293 20.707L20.707 19.293L13.4141 12L20.707 4.70703L19.293 3.29297L12 10.5859L4.70703 3.29297Z" fill="#FFFF"/>
                        </svg>
                    </button>
                </div>
                <div v-if="singleProduct.isActive">
                    <AssignProductQty
                        :selectedEmployee="selectedEmployee"
                        @employeeItemMappingUpdated="
                            this.$emit('employeeItemMappingUpdated')
                        "
                        @closeModal="closeModal(i)"
                        :selectedCategoryName="selectedCategoryName"
                    />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import AssignProductQty from "./AssignProductQty.vue";
export default {
    emits: ["closeAssignBtn", "closeModal", "employeeItemMappingUpdated"],
    props: ["selectedEmployee"],
    components: {
        AssignProductQty,
    },
    data() {
        return {
            products: [],
            filterProduct: [],
            uniqueProductCategory: {},
            selectedCategoryName: "",
            selectedIndex: -1
        };
    },
    mounted() {
        this.products = JSON.parse(
            localStorage.getItem("allProductsCategories")
        );
        // assign button filter area start
        for (let i in this.products) {
            for (let j in this.products[i].items) {
                let objCategory = this.products[i].items[j]["itemCategory"];
                this.uniqueProductCategory[objCategory] = this.products[i];
            }
        }
        // Loop to push unique object into array
        for (let i in this.uniqueProductCategory) {
            this.filterProduct.push(this.uniqueProductCategory[i]);
        }
        // assign button filter area end
    },
    methods: {
        closeModal(i) {
            this.$emit("closeModal");
            this.filterProduct[i]["isActive"] = false;
        },
        brandProductModal(value, i) {
            console.log(value);
            console.log(i);
            this.selectedIndex = i
            console.log('Selected Index:::', this.selectedIndex);
            // value.isActive = true
            this.filterProduct[i]["isActive"] = true;
            // this.selectedCategoryName = value.category
            this.selectedCategoryName = value;
        },
        closeItem (i) {
            this.filterProduct[i]["isActive"] = false
            this.selectedIndex = -1
        }
    },
};
</script>

<style lang="scss" scoped></style>
