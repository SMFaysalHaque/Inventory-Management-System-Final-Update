<template>

<nav>
  <div class="flex flex-wrap items-center justify-between my-2.5 w-full">
    <div class="logo">
      <p @click="name" class="font text-3xl font-bold">IMS</p>
    </div>
    <div class="list-topic">
      <ul class="flex">
        <li class="px-5 py-2 hover:bg-gray-400 hover:text-white rounded-sm text-lg ease-in duration-300"><a href="/">All Units</a></li>
        <li class="px-5 py-2 hover:bg-gray-400 hover:text-white rounded-sm text-lg ease-in duration-300"><a href="/person/">Persons</a></li>
        <li class="px-5 py-2 hover:bg-gray-400 hover:text-white rounded-sm text-lg ease-in duration-300"><a href="/unittypes/">Unit Types</a></li>
        <li class="px-5 py-2 hover:bg-gray-400 hover:text-white rounded-sm text-lg ease-in duration-300"><a href="/AvailableProduct/">Available Product</a></li>
        <li class="px-5 py-2 hover:bg-gray-400 hover:text-white rounded-sm text-lg ease-in duration-300"><a href="/TakenProduct/">Taken Product</a></li>
      </ul>
    </div>
    <div class="">
      <input class="border rounded-lg contrast-more:border-slate-400 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500 p-2" type="search" name="" id="" placeholder="Search Employee Name">
    </div>
  </div>
</nav>  
</template>

<script>
export default {
  data() {
    return {
    }
  },
    methods: {
      name() {
      }

    },
    mounted () {
      // console.log(this.counterValue);

    },
}
</script>

<style scoped>

</style>