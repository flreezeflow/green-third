<template>
    <div class="info w-screen mb-8">
        <div class="flex flex-col md:flex-row max-md:gap-16 justify-center">
            
            <div class="info_div mt-20 md:mt-5 ml-5 md:w-2/6 md:flex flex-col justify-center items-center">

                <div v-if="width === 'tablet' || width === 'non-mobile'" class="mb-3">
                    <div class="shadow-xl w-20 h-20 bg-white rounded-full flex justify-center items-center"><font-awesome-icon :icon="['fas', 'id-card']" class="text-blue-500 lg:text-lg" /></div>
                </div>

                <div class="flex flex-row gap-1 lg:text-2xl">
                    <h2 class="">What You Need <span class="text-white">To Apply</span></h2>
                    <!-- <h2 class="text-white">To Apply</h2> -->
                </div>
                <div class="md:w-full w-4/5 flex flex-row justify-between items-center gap-2 ml-5 md:ml-10">
                    
                    <div class="w-full md:h-32">
                        <div class="flex flex-row">
                            <ul class="flex flex-col gap-2 mt-3 list-disc">
                                <li class="text-sm"><p>3 Months latest bank statement for 1st time clients</p></li>
                                <li class="text-sm"><p>1 Month latest bank statement for existing clients</p></li>
                                <li class="text-sm"><p>Id copy</p></li>
                                <li class="text-sm"><p>Latest payslip</p></li>
                            </ul>
                            <div class="mt-3 w-3/5 md:w-1/5 md:ml-2">
                                <div class="border border-white w-0 h-full md:h-28"></div>
                            </div>
                        </div>
                    </div>

                    <div v-if="width === 'mobile'" class="mr-2">
                        <div class="shadow-xl w-16 h-16 bg-white rounded-full flex justify-center items-center"><font-awesome-icon :icon="['fas', 'id-card']" class="text-blue-500 text-lg" /></div>
                    </div>
                </div>
            </div>
            
            <div class="info_div md:mt-5 md:flex flex-col justify-center items-center md:w-2/6">
                <div v-if="width === 'tablet' || width === 'non-mobile'" class="mb-3">
                    <div class="shadow-xl w-20 h-20 bg-white rounded-full flex justify-center items-center"><font-awesome-icon :icon="['fas', 'calculator']" class="text-blue-500 text-2xl" /></div>
                </div>

                <div class="flex flex-row justify-end gap-1 lg:text-2xl">
                  <h2 class="mr-6">How Our <span class="text-white">Calculator Works</span></h2>
                </div>
                
                <div class="flex flex-row justify-between items-center gap-3 mr-5">
                    <div v-if="width === 'mobile'" class="mx-10 w-2/5">
                        <div class="shadow-xl w-16 h-16 bg-white rounded-full flex justify-center items-center"><font-awesome-icon :icon="['fas', 'calculator']" class="text-blue-500 text-2xl" /></div>
                    </div>
                    
                    <div class="w-4/5 md:h-32 md:w-full md:flex flex-row justify-between items-center gap-2 md:ml-8">

                        <div class="md:w-full">
                            <div class="flex flex-row">

                                <div v-if="width === 'mobile'" class="mt-3 w-1/5">
                                    <div class="info_line border border-white w-0 h-full"></div>
                                </div>

                                <ul class="mt-3 w-4/5 flex flex-col gap-3 list-disc ">
                                    <li class="text-sm"><p class="max-md:text-end">Use our loan calculator to guage how much is convenient for you</p></li>
                                    <li class="text-sm"><p class="max-md:text-end">Note that this amount might change after your loan is approved </p></li>
                                </ul>

                                <div v-if="width === 'tablet' || width === 'non-mobile'" class="mt-3 w-1/5 ml-2">
                                    <div class="border border-white w-0 h-28"></div>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                </div>
            </div>
            
            <div class="info_div md:ml-0 md:w-2/6 ml-5 md:flex flex-col justify-center items-center md:mt-5">
                <div v-if="width === 'tablet' || width === 'non-mobile'" class="mb-3">
                    <div class="shadow-xl w-20 h-20 bg-white rounded-full flex justify-center items-center"><font-awesome-icon :icon="['fas', 'pen']" class="text-blue-500 text-lg md:tex-2xl" /></div>
                </div>

                <div class="flex flex-row gap-1 lg:text-2xl">
                    <h2 class="ml-6">After You <span class="text-white">Apply</span></h2>
                </div>
                
                <div class="flex flex-row md:h-32 justify-between max-md:items-center ml-5">
                    <div class="md:w-full md:mt-4 w-3/5">
                        <div class="flex flex-row">
                            <ul class="flex flex-col gap-3 list-disc">
                                <li class="text-sm"><p>Loan approval within 24 hours</p></li>
                                <li class="text-sm"><p>We will contact you via email or message</p></li>
                            </ul>
                            <div v-if="width === 'mobile'" class="mx-2 2/5">
                                <div class="border border-white w-0 h-full"></div>
                            </div>
                        </div>
                    </div>

                    <div v-if="width === 'mobile'" class="mx-9 w-1/5">
                        <div class="shadow-xl w-16 h-16 bg-white rounded-full flex justify-center items-center"><font-awesome-icon :icon="['fas', 'pen']" class="text-blue-500 text-lg" /></div>
                    </div>
                </div> 
            </div>
        </div>
    </div>
    
</template>

<script setup>
import { computed } from 'vue';

const width = computed(() =>{
  if(window.innerWidth >= 1024){
    return 'non-mobile'
  }else if(window.innerWidth >= 768){
    return 'tablet'
  }else{
    return 'mobile'
  }
});

</script>