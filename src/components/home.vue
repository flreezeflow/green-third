<template>
  <div class="grid grid-cols-1 grid-rows-1 lg:grid-rows-1">
    <div class="ad w-screen mt-10 h-fit row-span-1">
      <div class="ad_layer w-screen h-36 lg:h-44 absolute">
        <div class="backdrop-blur-sm w-screen">
          <h2 class="text-center font-bold ">NEED A QUICK FINANCIAL HAND?</h2>
          <p class="text-center text-white font-semibold">Get a loan from us</p>
        </div>
        <div>

        </div>
        <div>

        </div>
      </div>
      <img class="w-full h-36 lg:h-44" src="../assets/piggy bank.jpg" alt="money">
      <div class="flex justify-center items-center">
        <div class="lg:absolute top-48 bg-white z-40 h-32 rounded-b-lg shadow-xl lg:w-4/5 w-screen rounded-lg flex flex-col justify-center flex-wrap">
          <p class="text-center">One of the <span class="text-limegreen">lowest rates</span> you can find at just <span class="text-limegreen">20%</span>. Check out our <span class="text-limegreen">calculator below</span>  to guage how much you will need </p>
        </div>
      </div>
    </div>
    
    <div class="flex flex-col lg:flex-row w-screen">
      <!-- <div class="w-1/5 h-full flex items-center">
        <div v-if="width === 'non-mobile'" class="-z-10 h-full rounded-br-lg rounded-tr-lg shadow-lg  bg-white">
          <p class="text-md ">Use our loan calculator to guage how big of a loan is convenient for your purposes</p>
        </div>
      </div> -->

      <div class="lg:mt-28 flex flex-col justify-center items-center max-lg:p-4 lg:w-screen">
        <div class="bg-gray-100 w-4/5 lg:w-2/5 h-32 mt-5 shadow-xl rounded-xl flex justify-center items-center flex-col">
          <p class="text-center mt-4 text-md">
            Loan Amount: N${{ amount1 }}
          </p>
          <input
            type="range"
            min="500"
            max="3000"
            step="50"
            v-model="amount1"
            class="slider1 w-4/5 lg:w-3/5 mt-12 appearance-none h-2 bg-gray-300 rounded-lg outline-none "
          />
        </div>

        <div class="flex flex-col justify-center items-center max-lg:w-4/5 w-2/5 h-32 lg:h-32 rounded-xl lg:mt-5">
          <div>
            <p class="text-center mt-4 text-lg">
              Repayment terms:
            </p>
            <p class="text-center mt-2">
              {{ months }} Month/s
            </p>
          </div>
          
          <input
            type="range"
            min="1"
            max="5"
            step="1"
            v-model="months"
            class="slider2 w-4/5 lg:w-3/5 mt-5 appearance-none h-2 bg-gray-300 rounded-lg outline-none"
          />
        </div>

        <div class="w-screen rounded-md h-20 flex flex-col justify-center items-center">
          <p class="ml-1">Monthly Installments</p>
          
          <div class="border border-greenline w-1/5 lg:w-1/6 h-10 flex items-center rounded-lg">
            <p class="ml-1 lg:text-lg ">N$ {{ installments }}</p>
          </div>
        </div>
        
        <div class="lg:mb-5 flex flex-row">
          <p class="text-gray-300 text-center">*This amount might change once your loan is approved</p>
        </div>
      </div>
    </div>

  </div>
  
</template>

<script setup>
import { ref, computed } from 'vue';

const amount1 = ref(500); // Principal loan amount
const months = ref(1); // Number of repayment months
const rate = 0.2; // Interest rate (20%)
const width = computed(() =>{
  if(window.innerWidth < 1024){
    return 'mobile'
  }else{
    return 'non-mobile'
  }
});

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