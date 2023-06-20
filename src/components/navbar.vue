<template>
    <nav>
        <div class="flex flex-wrap items-center justify-between my-2.5 w-full">
            <div class="logo">
                <p @click="name" class="font text-3xl font-bold">IMS</p>
            </div>
            <div class="list-topic">
                <ul class="flex">
                    <li
                        class="px-5 py-2 hover:bg-gray-400 hover:text-white rounded-sm text-lg ease-in duration-300"
                    >
                        <a href="/">All Units</a>
                    </li>
                    <li
                        class="px-5 py-2 hover:bg-gray-400 hover:text-white rounded-sm text-lg ease-in duration-300"
                    >
                        <a href="/person/">Persons</a>
                    </li>
                    <li
                        class="px-5 py-2 hover:bg-gray-400 hover:text-white rounded-sm text-lg ease-in duration-300"
                    >
                        <a href="/category/">Unit Types</a>
                    </li>
                    <li
                        class="px-5 py-2 hover:bg-gray-400 hover:text-white rounded-sm text-lg ease-in duration-300"
                    >
                        <a href="/AvailableProduct/">Available Product</a>
                    </li>
                    <li
                        class="px-5 py-2 hover:bg-gray-400 hover:text-white rounded-sm text-lg ease-in duration-300"
                    >
                        <a href="/TakenProduct/">Taken Product</a>
                    </li>
                </ul>
            </div>
            <div>
                <p class="hidden">Nothing</p>
            </div>
        </div>
    </nav>
</template>

<script>
export default {};
</script>

<style scoped></style>
