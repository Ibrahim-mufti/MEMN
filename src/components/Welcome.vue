<template>
  <header class="py-32 bg-nav">
    <div class="container">
        <h2 class="my-16 text-5xl">Welcome To MEMN's Dashboard</h2>
        <p class="w-[50%] mx-auto text-xl mb-14">Here you can See your Monthly Chart with respect to your income and Expenses you provided</p>
        <div id="Cards" class="flex flex-row justify-evenly">
            <div class="px-5 py-5 text-left borders w-[30%] flex flex-col items-center">
                <div class="w-[30%] mb-5">
                    <img src="../assets/expense.png">
                </div>
                <div class="text-xl text-white">
                    <h2 class="mb-3 font-bold text-3xl">Manage Your Expenses</h2>
                    <p class="mb-2">Having trouble managing your expenses or having difficulty saving up<br>Try Our Expense Managerment System in which you can manage your expenses without any hurdle with respect to your income</p>
                    <p class="mb-2">By <strong>adding </strong> <strong>Editing </strong>and <strong>Deleting</strong> You can manage you expenses </p>
                    <p class="mb-3">Click below to Manage your Expenses with ease </p>
                    <div class="flex justify-end"><a href="/Expense-manager" class="btn" >Read More</a></div>
                </div>
            </div>
            <div class="px-5 py-5 text-left borders w-[30%] flex flex-col items-center">
                <div class="w-[30%] mb-5">
                    <img src="../assets/cash.png" alt="">
                </div>
                <div class="text-xl text-white">
                    <h2 class="mb-3 font-bold text-3xl">Manage Your Income</h2>
                    <p class="mb-2">Let us have a look at your Income if you are having trouble managing your expenses<br>we will provide best possible chart to let you know where all of your income is Being used at</p>
                    <p class="mb-2">By <strong>Adding</strong> <strong>Modifying</strong> and <strong>Deleting</strong> you can manage your income precisely</p>
                    <p class="mb-3">Click below to Manage your income with ease </p>
                    <div class="flex justify-end"><a href="/Income-manager" class="btn" >Read More</a></div>
                </div>
            </div>
            <div class="px-5 py-5 text-left borders w-[30%] flex flex-col items-center">
                <div class="w-[30%] mb-5">
                    <img src="../assets/info.png" alt="">
                </div>
                <div class="text-xl text-white">
                    <h2 class="mb-3 font-bold text-3xl">About us?</h2>
                    <p class="mb-2">Welcome to our Monthly Expense Management System! Our platform is designed to help you effortlessly track and manage your monthly expenses.</p>
                    <p class="mb-2">With user-friendly features and intuitive design</p>
                    <p class="mb-3">Take control of your finances with us and experience a seamless approach to tracking, analyzing, and optimizing your expenses</p>
                    <div class="flex justify-end"><a href="/About" class="btn" >Read More</a></div>
                </div>
            </div>
        </div>
    </div>
  </header>
</template>

<script setup>
   
</script>

<style scoped>
    .container {
        width:100%;
        max-width: 1140px;
        margin-left:auto;
        margin-right:auto;
        text-align: center;
    }
    .borders{
        border-radius: 5px;
        border-top-left-radius: 50px;
        border-bottom-right-radius:50px ;
        background-color: black;       
        box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
    }
    @keyframes pop-up {
        0%{
            transform: translateY(0);
        }
        100%{
            transform: translateY(-30px);
            /* box-shadow: rgba(0, 0, 0, 0.56) 0px 22px 70px 4px; */
            /* box-shadow: rgba(169, 169, 169, 0.4) 0px 8px 24px */
        }
    }

    .borders:hover{
        animation: pop-up .3s forwards;
        box-shadow: rgba(200, 200, 200, 0.56) 0px 22px 70px 4px;
    }
    .btn{
        margin-top: 8px;
        padding: 10px 25px;
        background-color: rgb(32, 32, 32);
        border-top-right-radius: 30px;
        border-bottom-left-radius: 30px;
        color:black;
    }
    .btn:hover{
        border-radius: 0;
        border-top-left-radius: 30px;
        border-bottom-right-radius: 30px;
        background-color: white;
        color:black;
        transition: all .3s ease-in;
    }
    #Cards p{
        color:rgb(173, 173, 173)
    }
 </style>