<template>
    <div>
        <div class="w-full bg-gray-100 h-screen my-5 rounded-md">
            <p class="font-bold text-md ms-5 pt-5">Taken Products</p>
            <table
                class="table-auto w-[90%] mx-auto mt-5 border-collapse border border-slate-300"
            >
                <thead>
                    <tr class="h-10 bg-gray-300 border-b-2 border-gray-400">
                        <th class="border border-slate-200">Employee Name</th>
                        <th class="border border-slate-200">E-mail</th>
                        <th class="border border-slate-200">Category</th>
                        <th class="border border-slate-200">Brand</th>
                        <th class="border border-slate-200">Model</th>
                        <th class="border border-slate-200">Taken Quantity</th>
                    </tr>
                </thead>
                <tbody>
                    <tr
                        v-for="takenSingleProduct in takenProduct"
                        :key="takenSingleProduct"
                    >
                        <td class="border border-slate-200 text-center">
                            {{ takenSingleProduct.employeeName }}
                        </td>
                        <td class="border border-slate-200 text-center">
                            {{ takenSingleProduct.employeeEmail }}
                        </td>
                        <td class="border border-slate-200 text-center">
                            {{ takenSingleProduct.itemCategory }}
                        </td>
                        <td class="border border-slate-200 text-center">
                            {{ takenSingleProduct.itemBrand }}
                        </td>
                        <td class="border border-slate-200 text-center">
                            {{ takenSingleProduct.itemModel }}
                        </td>
                        <td class="border border-slate-200 text-center">
                            {{ takenSingleProduct.itemQuantity }}
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            // key: value
            takenProduct: [],
        };
    },
    mounted() {
        // get localStorage:
        this.takenProduct = JSON.parse(
            localStorage.getItem("employeeItemMapping")
        )
            ? JSON.parse(localStorage.getItem("employeeItemMapping"))
            : [];
    },
};
</script>

<style lang="scss" scoped></style>
