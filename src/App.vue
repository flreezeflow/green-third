<template>
  <header class="">
    <div class="bg-white shadow-xl w-screen h-10 fixed z-50 left-0 top-0 ">
      <ul class="ml-2 text-sm">
        <div class="nav2 flex flex-row justify-between align-center">
          <div class="logo">
            <!-- <img src="./assets/Asset 19-20.jpg" alt="" class="w-4/5"> -->
            <p class="text-2xl">Logo here</p>
          </div>
        </div>
      </ul>
    </div>
  </header>

  <div class="grid grid-cols-1 md:grid-rows-2">
    <div class="shadow-lg home w-screen mt-1 bg-white">
      <home/>
    </div>
    <!-- <div class="trans-pic shadow-inner w-screen h-4/5 absolute flex justify-center items-center">
      <div class="z-10 absolute"></div>
      <img src="./assets/money pic.jpg" alt="" class="h-3/5 w-screen fixed">
    </div> -->
    <div class="info w-screen h-fit">
      <info/>
    </div>
    <div class="shadow-lg apply bg-gradient-to-b from-greenline from-20% via-white via-10% to-white to-60% w-screen">
      <apply/>
    </div>
    <div class="about w-screen">
      <about/>
    </div>
    <!-- <div class="footer w-screen z-50 mt-8">
      <greenlinefooter/>
    </div> -->
  </div>
</template>

<script setup>
import home  from "./components/home.vue";
import apply  from "./components/apply.vue";
import info from './components/info.vue';
import about from "./components/about.vue"
import greenlinefooter from "./components/footer.vue"
</script>