<template>
  <header class="">
    <div class="bg-white shadow-xl w-screen h-12 fixed z-50 left-0 top-0">
      
      <div class="flex flex-row items-center">
        <div class="w-screen h-12 flex justify-start">
          <img src="./assets/Asset 3.svg" alt="" class="w-3/5 h-4/5">
        </div>
        <div @click="toggleContact" :class="togglerClass" class="mr-6 bg-limegreen w-12 h-9 rounded-full flex justify-center items-center cursor-pointer">
          <font-awesome-icon :icon="['fas', togglerIcon]" class="text-white "/>
        </div>
      </div>
      
      <div v-if="contact === 'opened'" class="flex justify-end">
        <div :class="contactClass" class="flex flex-row justify-center items-center h-5 lg:h-7 rounded-bl-lg bg-white shadow-xl ">
          <p class="text-sm lg:text-lg">{{ contactInfo }}</p>
        </div>
      </div>
    </div>
  </header>

  <div class="grid md:grid-rows-1">
    <div class="shadow-lg home w-screen mt-1">
      <home/>
    </div>
    <div class="info w-screen h-fit">
      <info/>
    </div>
    <div class="shadow-lg bg-white apply bg-gradient-to-b from-greenline from-20% lg:from-40% via-white via-10% to-white to-60% w-screen">
      <apply/>
    </div>
    <div class="about w-screen">
      <about/>
    </div>
    <div class="footer bg-greenline w-screen z-50 lg:mt-16">
      <greenlinefooter/>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

import home  from "./components/home.vue";
import apply  from "./components/apply.vue";
import info from './components/info.vue';
import about from "./components/about.vue"
import greenlinefooter from "./components/footer.vue"

let contact = ref('closed');
let contactClass = ref('')
let contactInfo = ref('');
let togglerClass = ref('toggled');
let togglerIcon = ref('phone');

function toggleContact(){
  if(contact.value === 'closed'){
    contact.value = 'opened'
    togglerIcon.value = 'envelope'
    contactInfo.value = '0818669984'
    contactClass = 'w-32 lg:w-40'
  }else if(contact.value === 'opened' && togglerIcon.value === 'envelope'){
    togglerIcon.value = 'arrow-left-long'
    contactInfo.value = 'greenline@gmail.com'
    contactClass = 'w-40 lg:w-52'
  }else{
    contact.value = 'closed'
    togglerIcon.value = 'phone'
    contactInfo.value = ''
  }
}

</script>