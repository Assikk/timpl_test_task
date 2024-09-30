<template>
  <div class="fixed top-0 bg-[#00000060] left-0 w-full h-full z-10 flex items-center justify-center">
    <div class="bg-white text-center rounded-md p-3 flex flex-col gap-4 w-full mx-[28px]">
        <div class="relative">
            <img src="../../assets/img/carbon.jpg" alt="SWEN">
            <div class="absolute right-2 top-2 w-8 h-8 bg-white rounded-full flex items-center justify-center">
                <svg width="24" height="24" iewBox="0 0 24 24" fill="#262D35"
                @click="$emit('close')">
                  <use xlink:href="#close"/>
                </svg>
            </div>
        </div>
        <div>
            <h3 class="font-medium text-lg text-[#262D35] mb-2">
            Profit goes to SWEN 
            </h3>
            <p  class="text-[17px] text-[#808191] leading-[24px]">
                By leaving a tip, you take care of nature
            </p>
        </div>
        <Button>
            Learn more about SWEN
        </Button>
    </div>
  </div>
</template>
<script>
import Button from '../buttons/default.vue'
export default {
    name: 'SwenModalComponent',
    components: {
        Button
    }
}
</script>