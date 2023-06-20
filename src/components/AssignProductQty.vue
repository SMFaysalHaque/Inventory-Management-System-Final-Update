<template>
    <div>
        <!-- :disabled="" -->
        <div class="border-b-2 w-auto">
            <div
                v-for="(singleBrand, index) in brand"
                :key="singleBrand"
                class="flex justify-between items-center my-1"
            >
                <p>{{ singleBrand.itemBrand }}</p>
                <p>{{ singleBrand.itemModel }}</p>
                <div>
                    <button
                        @click="minusButton(index)"
                        class="border border-gray-500 px-3 py-0 me-2 hover:bg-stone-300 ease-in duration-200"
                    >
                        -
                    </button>
                    <span>{{ counters[index] }}</span>
                    <button
                        @click="
                            plusButton(
                                singleBrand.itemQuantity,
                                singleBrand.itemModel,
                                index
                            )
                        "
                        class="border border-gray-500 px-3 py-0 ms-2 hover:bg-gray-300 ease-in duration-200"
                    >
                        +
                    </button>
                </div>
                <div>
                    <button
                        @click="
                            addAndCloseProductBrand(
                                singleBrand.itemBrand,
                                singleBrand.itemModel,
                                index
                            )
                        "
                        class="border border-green-700 bg-green-700 hover:bg-green-500 hover:border-green-500 rounded-sm text-white px-2"
                    >
                        add
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Category from "../components/Category.vue";
export default {
    components: {
        Category,
    },
    emits: ["close", "closeModal", "employeeItemMappingUpdated"],
    props: {
        selectedCategoryName: {
            type: String,
            default: null,
        },
        closeCategory: {
            type: Boolean,
            default: false,
        },
        selectedEmployee: {
            type: Object,
            default: null,
        },
    },
    data() {
        return {
            counters: [],
            allItems: [],
            brand: [],
            employeeItemMapping: [],
            availableProduct: 0,
            isVisibleProductBrand: false,
        };
    },
    mounted() {
        this.allItems = JSON.parse(
            localStorage.getItem("allProductsCategories")
        );
        let element;
        for (let index = 0; index < this.allItems.length; index++) {
            for (let j = 0; j < this.allItems[index].items.length; j++) {
                element = this.allItems[index].items[j].itemCategory;
                if (this.selectedCategoryName === element) {
                    let allBrand = this.allItems[index].items[j];
                    this.brand.push(allBrand);
                } else {
                    console.log("what????????");
                }
            }
        }

        for (let i = 0; i < this.brand.length; i++) {
            this.counters.push(0);
        }
    },
    methods: {
        minusButton(i) {
            if (this.counters[i] > 0) {
                this.counters[i]--;
            }
        },
        plusButton(value, model, i) {
            console.log(value);

            // get localStorage
            let employeesAssignUnits = JSON.parse(
                localStorage.getItem("employeeItemMapping")
            )
                ? JSON.parse(localStorage.getItem("employeeItemMapping"))
                : [];

            // button available limitation
            let totalTaken = 0;
            employeesAssignUnits.forEach((quantity) => {
                if (quantity.itemModel === model) {
                    totalTaken = totalTaken + quantity.itemQuantity;
                }
            });
            this.availableProduct = value - totalTaken;
            if (this.counters[i] < this.availableProduct) {
                this.counters[i]++;
            } else if (this.availableProduct == 0) {
                this.isVisibleProductBrand = false;
            }

            //     this.allProductsSummary.forEach((el1) => {
            //     let reserveCategory = el1.categoryName;
            //     let allQuantity = el1.categoryQuantity;
            //     let totalTaken = 0;

            //     this.employeesAssignUnits.filter((el2) => {
            //         if (reserveCategory === el2.itemCategory) {
            //             totalTaken = totalTaken + el2.itemQuantity;
            //         }
            //     });
            //     el1.totalTakenQuantity = totalTaken;
            //     el1.totalAvailableQuantity = allQuantity - totalTaken;
            // });
        },
        addAndCloseProductBrand(brand, model, i) {
            this.$emit("closeModal");
            this.brand[i].isActive = !this.brand[i].isActive;

            //parse assignedItem:
            let employeeItemMapping = JSON.parse(
                localStorage.getItem("employeeItemMapping")
            )
                ? JSON.parse(localStorage.getItem("employeeItemMapping"))
                : [];

            if (this.selectedEmployee === null) {
                console.log("No selected employee.");
                return;
            }
            const assignedItem = {
                employeeName: this.selectedEmployee.name,
                employeeEmail: this.selectedEmployee.email,
                itemCategory: this.selectedCategoryName,
                itemBrand: brand,
                itemModel: model,
                itemQuantity: this.counters[i],
            };
            employeeItemMapping.push(assignedItem);
            localStorage.setItem(
                "employeeItemMapping",
                JSON.stringify(employeeItemMapping)
            );
            this.$emit("employeeItemMappingUpdated");
        },
    },
};
</script>

<style lang="scss" scoped></style>
