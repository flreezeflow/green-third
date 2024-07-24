<template>
  <header class="">
    <div class="bg-white shadow-xl w-screen h-10 fixed z-50 left-0 top-0 ">
      <ul class="ml-2 text-sm">
        <div v-if="nav === 'nav1'" class="nav1 mt-2 flex flex-row flex-wrap justify-around flex-grow">
          <li>
            <button @click="underline('line')">Home</button>
            <div :class="line"></div>
          </li>
          <li>
            <button @click="underline('line2')">Info</button>
            <div :class="line2"></div>
          </li>
          <li>
            <button @click="underline('line1')">Apply</button>
            <div :class="line1"></div>
          </li>
          
          <li>
            <button @click="underline('line3')">Contact</button>
            <div :class="line3"></div>
          </li>
          <li>
            <button class="ml-5 w-10 rounded-lg bg-greenline shadow" @click="changeNav"><-</button>
          </li>
        </div>

        <div @click="changeNav" v-if="nav === 'nav'" class="nav2 flex flex-row justify-between align-center">
          <div class="logo">
            <!-- <img src="./assets/Asset 19-20.jpg" alt="" class="w-4/5"> -->
            <p class="text-2xl">Logo here</p>
          </div>
          <div class="burgers mr-5 mt-3">
            <div class="ml-2 w-4 border border-greenline border-solid"></div>
            <div class="w-8 my-1 border border-greenline border-solid"></div>
            <div class="ml-2 w-4 border border-greenline border-solid"></div>
          </div>
        </div>
      </ul>
    </div>
  </header>

  <div class="grid grid-cols-1 md:grid-rows-2">
    <div class="home w-screen mt-1">
      <home/>
    </div>
   <div class="info w-screen">
      <info/>
    </div>
    <div class="shadow-lg apply bg-gradient-to-b from-greenline from-20% via-white via-10% to-white to-60% w-screen">
      <apply/>
    </div>
    <div class="about w-screen">
      <about/>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import home  from "./components/home.vue";
import apply  from "./components/apply.vue";
import info from './components/info.vue';
import about from "./components/about.vue"

let nav = ref('nav')
let page = ref('home')

const line = ref('line')
const line1 = ref('')
const line2 = ref('')
const line3 = ref('')

function underline(selectedLine) {
  line.value = ''
  line1.value = ''
  line2.value = ''
  line3.value = ''
  
  switch (selectedLine) {
    case 'line':
      line.value = 'line'
      page.value = 'home'
      break
    case 'line1':
      line1.value = 'line'
      page.value = 'apply'
      break
    case 'line2':
      line2.value = 'line'
      page.value = 'info'
      break
    case 'line3':
      line3.value = 'line'
      page.value = 'contact'
      break
  }
}

function changeNav() {
  nav.value = nav.value === 'nav' ? 'nav1' : 'nav'

}

console.log(nav.value)

</script>