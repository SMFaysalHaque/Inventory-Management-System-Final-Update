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
                :key="singleProduct"
                class=""
            >
                <div class="flex justify-between items-center py-1">
                    <p>{{ singleProduct.categoryName }}</p>
                    <button
                        @click="
                            brandProductModal(singleProduct.categoryName, i)
                        "
                        class="border border-green-700 bg-green-700 hover:bg-green-500 hover:border-green-500 rounded-sm text-white px-2"
                    >
                        add
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
        addModel() {},
        closeModal(i) {
            this.$emit("closeModal");
            this.filterProduct[i]["isActive"] = false;
        },
        brandProductModal(value, i) {
            console.log(value);
            // value.isActive = true
            this.filterProduct[i]["isActive"] = true;
            // this.selectedCategoryName = value.category
            this.selectedCategoryName = value;
        },
    },
};
</script>

<style lang="scss" scoped></style>
