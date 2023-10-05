<template>
    <header class="py-32">
        <div class="container">
            <div class="mb-5">
                <h2 class="text-4xl font-bold mb-5">Expense Manager</h2>
                <p class="w-[75%] mx-auto text-2xl">Manage your expenses by categorizing them According the way you want the to manage By simply Adding, Modifying and Deleting</p>
            </div>
            <form class="w-[40%] mx-auto py-10 " @submit.prevent="onSubmit">
                <div class="mx-5 flex flex-col justify-start mb-5">
                    <label class="font-bold text-2xl mb-3 text-left" for="Expenses">Enter your Expense</label>
                    <input class="outline-none border-b-2 text-lg py-2 px-4" type="text" v-model="text" placeholder="Enter your Expense Here">
                </div>
                <div class="mx-5 flex flex-col mb-5">
                    <label class="font-bold text-2xl mb-3 text-left" for="Budget">Enter price of that Expense</label>
                    <input class="outline-none border-b-2 text-lg py-2 px-4" type="number" v-model="number" placeholder="Enter price of the expense">
                </div>
                <div class="flex justify-end">
                    <button class="text-2xl py-3 px-6 rounded-[20px] bg-slate-700 text-white" type="submit">Submit</button>
                </div>
            </form>
            <!-- Displaying data that is being added to data base  -->
            <div class="w-full text-center" v-for="val in ExpenseData" :key="val">
               <div class="w-[30%] mx-auto bg-slate-300 mb-3 flex flex-row items-center rounded-[20px] "> 
                    <h2 class="text-xl mx-3 py-3 pr-3 border-r-2">{{ val.Expense }}</h2>
                    <h2 class="text-xl mx-3 py-3 pr-3">{{ val.Price}}</h2>
                    <!-- Removing the Entitty from the database as well as the frontend -->
                    <div class="flex w-full mr-5 text-xl text-red-600 justify-end ">
                        <button @click="deletedata(val.id)" class="py-2 px-4 bg-slate-600 text-white">X</button>
                    </div>
                </div>
            </div>
        </div>
    </header>
</template>

<script setup>
// Importing

    import { onMounted, ref } from 'vue'; 
    import { collection, addDoc,deleteDoc, doc,onSnapshot, query, orderBy } from 'firebase/firestore';
    import { db } from "../main"

// Variable decleration

    const text = ref("");  
    const number = ref("");
    const ExpenseData = ref([])
    let customId = 1

// Functions  
    // on submission the data will be send to database 
    const onSubmit = async() => {

        // if Expense exist then add data on it otherwise it will create the database collection 
        const expenseRef = collection(db, "Expenses"); 
        if(text.value == "" && number.value == ""){
            alert("Fields cannot be empty")
        }
        else{
        // adding data into EXPENSES database with following Values
            await addDoc(expenseRef, {
                customId : customId,
                Expense : text.value,
                Price : number.value,
            })
        }
    // ExpenseData.value.push({customId : customId, Expense : text.value, Price : number.value})
    // increasing the value of customID however (i will not use it later)
    customId++ 
    // restating the vaalue of input field as empty 
    text.value = ""
    number.value = ""

    }

    // deleting the specific data fron the database
    const deletedata = async(id) => {

        // checking document with id only  
        const expenseRef = doc(db, "Expenses", id);

        // deleting the entity with the specific id passes from the button
        await deleteDoc(expenseRef);

        // what this is doing is iterating through whole ExpenseData and checking for the condition with the help of filter() what filter doing is 
        // iterating with a specific condition if the condition implies is true it will add the data to the array and if false it will exclude that data 
        // thus ExpenseData will now have a new array without the excluded value 
        ExpenseData.value = ExpenseData.value.filter(item => item.id !== id);
    }
    onMounted(async() => {

        // if Expense exist then add data on it otherwise it will create the database collection 
        const expenseRef = collection(db, "Expenses")

        // to perform real time modification on a query  (will watch a video about it)
        onSnapshot(query(expenseRef, orderBy("customId", "asc")), (QuerySnapshot) => {
                ExpenseData.value=[]
                QuerySnapshot.forEach((doc) => {
                ExpenseData.value.push({id: doc.id, ...doc.data()})
            })
        })
    })
</script>

<style scoped>
.container {
    width:100%;
    max-width: 1140px;
    margin-left:auto;
    margin-right:auto;
    text-align: center;
}
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
}
</style>
