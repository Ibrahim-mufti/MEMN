<template>
    <section class="py-5 w-full fixed">
        <div class="container ">
            <div class="flex flex-row justify-between">
                <div class="w-1/4">
                    <div class="flex flex-row items-center">
                        <img class="w-[120px]" src="../assets/logo_transparent.png">
                        <p class="text-4xl ml-[-20px] text-white">ME<e class="font-extrabold">MN</e></p>
                    </div>
                </div>
                <ul id="Dash_items" class="w-3/5 text-clr flex flex-row justify-around text-lg items-center">
                    <li><a href="/dashboard">Dashboard</a></li>
                    <li><a href="/Expense-manager">Expense Manager</a></li>
                    <li><a href="/Income-manager">Income Manager</a></li>
                    <li><a href="/About">About</a></li>
                    <button @click="handleSignOut" class="py-2 px-4 text-xl border rounded-full bg-transparent ">Sign Out</button>
                </ul>
            </div>
        </div>
    </section>
    <Welcome/>
    <Charts/>
</template>

<script setup>

// Imports
    import Charts from "../components/Charts.vue"
    import Welcome from "../components/Welcome.vue"
    import { onMounted,ref } from 'vue';
    import {getAuth, onAuthStateChanged, signOut} from "firebase/auth"
    import router from '@/router';

// Variables
    const isloggedin = ref(false)
    let auth

// Functions 

    // Will Load as soon as the DOM is loaded 
    onMounted(() => {
        auth = getAuth()

        // Calling the OnAuthstateCHangemethod 
        // which will check if the user has logged in or not
        onAuthStateChanged(auth, (user) => {
            if(user) {
                isloggedin.value = true
            }
            else {
                isloggedin.value = false
            }
        })
    })

    // Clicking on Sign Out will move the user back to the Sign In page
    const handleSignOut = () => {
            signOut(auth).then(() => {
                router.push("/")
        })
    }

</script>

<style scoped>
  .container {
        width:100%;
        max-width: 1140px;
        margin-left:auto;
        margin-right:auto;
        text-align: center;
    }
    #Dash_items button:hover{
        background-color: white;
        color:#04619f;
        transition: all .7s ease-in;
    }
    #Dash_items li:hover{
        color:white;
        transition: all .5s ease-in;
    }
</style>