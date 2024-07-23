<template>
    <div class="info w-screen bg-greenline">
        <div class=" flex flex-col gap-16 justify-center">
            <div class="info_div mt-20 ml-5">
                <h2 class="underline ">What You Need To Apply</h2>
                
                <div class="w-4/5 flex flex-row justify-between items-center gap-2 ml-5">
                    
                    <div class="w-4/5">
                        <div class="flex flex-row">
                            <ul class="flex flex-col gap-3 mt-3">
                                <li class="text-sm"><p>3 Months latest bank statement</p></li>
                                <li class="text-sm"><p>Certified Id copy</p></li>
                                <li class="text-sm"><p>Latest payslip</p></li>
                            </ul>
                            <div class="mt-3 w-3/5">
                                <div class="border border-white w-0 h-full"></div>
                            </div>
                        </div> 
                    </div>

                    <div class="mr-2 1/5">
                        <div class="shadow-xl w-16 h-16 bg-white rounded-full flex justify-center items-center"><font-awesome-icon :icon="['fas', 'id-card']" class="text-blue-500 text-lg" /></div>
                    </div>
                </div>
            </div>
            


            <div class="info_div">
                <h2 class="underline text-end mr-6">How Our Calculator Works</h2>
                
                <div class="flex flex-row justify-between items-center gap-3 mr-5">
                    <div class="mx-10 w-2/5">
                        <div class="shadow-xl w-16 h-16 bg-white rounded-full flex justify-center items-center"><font-awesome-icon :icon="['fas', 'calculator']" class="text-blue-500 text-2xl" /></div>
                    </div>
                    
                    <div class=" w-4/5">
                        <div class="flex flex-row">
                            <div class="mt-3 w-2/5">
                                <div class="info_line border border-white w-0 h-full"></div>
                            </div>
                            <ul class="mt-3 flex flex-col gap-3">
                                <li class="text-sm"><p class="text-end">Use our loan calculator to guage how much is convenient for you</p></li>
                                <li class="text-sm"><p class="text-end">Note that this amount might change after your loan is approved </p></li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>
            


            <div class="info_div ml-5">
                <h2 class="underline ml-5">After you apply</h2>
                <div class="flex flex-row justify-between items-center ml-5">
                    <div class="w-3/5">
                        <div class="flex flex-row">
                            <ul class="flex flex-col gap-3">
                                <li class="text-sm"><p>2~3 Weeks until loan approval or denial</p></li>
                                <li class="text-sm"><p>Appon aproval or denial of your appication, you will be notified via email or message</p></li>
                            </ul>
                            <div class="mx-2 2/5">
                                <div class="border border-white w-0 h-full"></div>
                            </div>
                        </div>
                    </div>

                    <div class="mx-9 w-1/5">
                        <div class="shadow-xl w-14 h-14 bg-white rounded-full flex justify-center items-center"><font-awesome-icon :icon="['fas', 'pen']" class="text-blue-500 text-lg" /></div>
                    </div>
                </div> 
            </div>
            

        </div>
    </div>
    
</template>