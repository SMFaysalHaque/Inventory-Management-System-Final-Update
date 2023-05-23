<template>
    <div>
        <div class="headline-searchBar my-2.5">
        <p class="font-bold text-lg">Persons</p>
    </div>

    <div class="grid grid-cols-12 border border-cyan-700 bg-slate-100">
        <div class="col-span-1 ms-2 border-e-2">
            <p>Employee Serial No.</p>
        </div>
        <div class="flex items-center justify-center col-span-3 border-e-2">
            <p>Employee Info.</p>
        </div>
        <div class="flex items-center justify-center col-span-5 border-e-2">
            <p>All Units</p>
        </div>
        <div class="flex items-center justify-center col-span-3">
            <p>Assign Units</p>
        </div>
    </div>
     
    <div v-for="(personInfo, i) in personInfos" :key="i" class="grid grid-cols-12 border border-cyan-700">
        <div class="flex justify-center items-center col-span-1 border-e-2">
            <p>{{ i+1 }}</p>
        </div>
        <div class="flex flex-col justify-center ps-10 space-y-3 col-span-3 border-e-2">
            <p>Name: {{ personInfo.name }}</p>
            <p>Mobile: {{ personInfo.mobile }}</p>
            <p>E-mail: {{ personInfo.email }}</p>
        </div>
        <div class="col-span-5 border-e-2">
            <table class="table-fixed mx-5 my-5 w-11/12">
                <thead>
                    <tr>
                        <th class="border border-slate-300 bg-slate-100 w-6/12 py-2 text-center">Type</th>
                        <th class="border border-slate-300 bg-slate-100 w-6/12 py-2 text-center">Quantity</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(value, key) in personInfo.device" :key="value">
                        <!-- {{ personInfo.device }} -->
                        <td class="border border-slate-300 text-center py-3">{{ key }}</td>
                        <td class="border border-slate-300 text-center py-3">{{ value }}</td>
                    </tr>
                </tbody>
            </table>
        </div>
        <div class="flex flex-col items-center justify-center col-span-3 mx-5 my-5">
            <button class="border rounded-lg contrast-more:border-slate-400 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500 hover:bg-sky-600 hover:text-white px-10 py-3 me-2 ease-in duration-300" @click="isShowed(i)">Assign Units</button>
            <div v-if="personInfo.show">
                <AssignItem @assignProduct="assignProduct($event, i)" @close="isClosed(i)"/>
            </div>
        </div>
    </div>
    
    </div>
</template>

<script>
import AssignItem from '../components/AssignItem.vue'
    export default {
        components: {
            AssignItem,
        },
        data() {
            return {
                // isModalVisible: false,
                personInfos: [],
                // selectedIndex: -1,
            }
        },
        mounted(){
            this.personInfos = JSON.parse(localStorage.getItem('allEmployee'));
            this.personInfos.forEach(element => {
                element.show = false
            });

            
            // console.log(this.personInfos)
            // for (let index = 0; index < this.personInfos.length; index++) {
            //     const element = this.personInfos[index].device.type;
            //     console.log(element)
            // }

        },
        methods: {
            // addData(value) {
            //     value= JSON.parse(JSON.stringify(value))
            //     value.device.name="mouse"
            //     value.device.quantity=1
            //     console.log(value.device)
            // }
            isShowed(index){
                // this.selectedIndex = index
                // console.log(this.personInfos[index])
                this.personInfos[index].show = true
            },
            isClosed(index){
                this.personInfos[index].show = false
                // this.isModalVisible = true
                // this.selectedIndex = index
            },
            assignProduct(type, index){
                console.log("typpe", type , "index", index);
                const currentPerson = this.personInfos[index]
                console.log(currentPerson)
                if(!currentPerson.device[type]){
                    currentPerson.device[type] = 1;
                }
                // else{
                //     currentPerson.device[type] = 
                // }
                console.log("currentPerson", currentPerson);
                localStorage.setItem('allEmployee', JSON.stringify(this.personInfos))


                // console.log("typpe", type , "index", index);
                // //get type quantity                                                 
                // const allProducts = localStorage.getItem('allProductDetails')
                // let typeQuantity = 0
                // for (let index = 0; index < allProducts.length; index++) {
                //     const product = allProducts[index];
                //     if (product.type === type) {
                //         typeQuantity = product.quantity
                //     }
                // }
                // // count number of taken units
                // let takenUnits = 0
                // for (let index = 0; index < this.personInfos.length; index++) {
                //     const person = this.personInfos[index];
                //     takenUnits = takenUnits + person.device[type]
                // }
                // // if product available assign it to person else give alert
                // if (takenUnits <= typeQuantity){
                
                //     const currentPerson = this.personInfos[index]
                //     if(!currentPerson.device[type]){
                //         currentPerson.device[type] = 1;
                //     }
                //     else{
                //         currentPerson.device[type] = currentPerson.device[type] + 1
                //     }
                //     console.log("currentPerson", currentPerson);
                //     localStorage.setItem('allEmployee', JSON.stringify(this.personInfos))
                // }
                // else{
                //     alert(`${type} is not available`)
                // }
            }
        }
    }
</script>