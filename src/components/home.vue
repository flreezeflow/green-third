<template>
  <div class="grid grid-cols-1 grid-rows-3">
    <div class="ad mt-10 h-72 row-span-1">
      <div class="absolute top-48 bg-white z-40 h-32 rounded-b-lg shadow-xl w-screen flex flex-col justify-center">
        <p class="text-center text-md ">Use our loan calculator to guage how big of a loan is convenient for your purposes</p>
      </div>
      <div class="bg-greenline w-screen h-36 absolute opacity-30 shadow-inner">
        <p class="mt-16 text-center font-semibold">
          Everyday loans for the average joe
        </p>
      </div>
      <img class="w-full h-36" src="../assets/piggy bank.jpg" alt="money">
    </div>
    <div class="flex flex-col items-center p-4 row-span-2">
      <div class="bg-gray-100 w-4/5 h-32 shadow-xl rounded-xl flex justify-center flex-col">
        <p class="text-center mt-4 text-md">
          Loan Amount: N${{ amount1 }}
        </p>
        <input
          type="range"
          min="500"
          max="3000"
          step="50"
          v-model="amount1"
          class="slider1 w-4/5 ml-7 mt-12 appearance-none h-2 bg-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
        />
      </div>

      <div class="w-4/5 h-44 rounded-xl ">
        <p class="text-center mt-4 text-lg">
          Repayment terms:
        </p>
        <p class="text-center mt-2">
          {{ months }} Month/s
        </p>
        <input
          type="range"
          min="1"
          max="5"
          step="1"
          v-model="months"
          class="slider2 w-4/5 ml-7 mt-12 appearance-none h-2 bg-gray-300 rounded focus:outline-none focus:ring-2 focus:ring-blue-500"
        />
      </div>

      <div class="w-screan rounded-md h-20 flex flex-col justify-center ">
        <p class="ml-1">Monthly Installments</p>
        
        <div class="border border-greenline w-full h-10 flex items-center rounded-lg">
          <p class="ml-1">N$ {{ installments }}</p>
        </div>
      </div>

      <div class="mt-5 flex flex-row">
        <p class="font-semibold">Note:</p>
        <p class="text-red-800">This amount might change once your loan is approved</p>
      </div>
    </div>
  </div>
  
</template>

<script setup>
import { ref, computed } from 'vue';

const amount1 = ref(500); // Principal loan amount
const months = ref(1); // Number of repayment months
const rate = 0.2; // Interest rate (20%)

const installments = computed(() => {
  if (months.value <= 0) {
    return amount1.value; // Immediate payment, no interest calculation
  } else {
    const interest = parseFloat(amount1.value) * rate; // Calculate the interest
    const totalAmount = parseFloat(amount1.value) + interest; // Total amount including interest
    return totalAmount / months.value; // Monthly installment amount
  }
});

</script>

<style>
  .slider1{
    height: 12px;
    background-color: #fff;
    border: 1px solid #1efd00;
  }

  .slider1::-webkit-slider-thumb {
    -webkit-appearance: none;
    appearance: none;
    width: 25px;
    height: 25px;
    background: #1efd00;
    cursor: pointer;
    border-radius: 50%;
    border: 2px solid #1efd00;
  }

  .slider2{
    height: 12px;
    background-color: #1efd00;
  }

  .slider2::-webkit-slider-thumb {
    -webkit-appearance: none;
    appearance: none;
    width: 25px;
    height: 25px;
    background: #fff;
    cursor: pointer;
    border-radius: 40%;
    border: 2px solid #1efd00;
  }
</style>