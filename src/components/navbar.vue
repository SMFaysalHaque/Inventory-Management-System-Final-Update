<template>
    <nav class="sticky top-0 z-50 bg-white py-1">
        <div class="flex flex-wrap items-center justify-between my-2.5 w-full relative">
            <div class="logo">
                <p @click="name" class="font text-3xl font-bold">IMS</p>
            </div>
            <div class="list-topic">
                <ul class="flex">
                    <a href="/">
                        <li
                            class="px-5 py-2 hover:bg-gray-400 hover:text-white rounded-sm text-lg ease-in duration-300"
                        >
                            All Units
                        </li>
                    </a>
                    <a href="/person/">
                        <li
                            class="px-5 py-2 hover:bg-gray-400 hover:text-white rounded-sm text-lg ease-in duration-300"
                        >
                            Persons
                        </li>
                    </a>
                    <a href="/category/">
                        <li
                            class="px-5 py-2 hover:bg-gray-400 hover:text-white rounded-sm text-lg ease-in duration-300"
                        >
                            Unit Types
                        </li>
                    </a>

                    <a href="/AvailableProduct/">
                        <li
                            class="px-5 py-2 hover:bg-gray-400 hover:text-white rounded-sm text-lg ease-in duration-300"
                        >
                            Available Product
                        </li>
                    </a>

                    <a href="/TakenProduct/">
                        <li
                            class="px-5 py-2 hover:bg-gray-400 hover:text-white rounded-sm text-lg ease-in duration-300"
                        >
                            Taken Product
                        </li>
                    </a>
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
