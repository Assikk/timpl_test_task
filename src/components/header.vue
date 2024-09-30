<template>
    <header>
        <div class="flex gap-4 py-3 px-5 bg-white">
            <div class="flex-1 flex justify-center">
                <img src=".././assets/img/logo.svg" alt="">
            </div>
            <Select id="lang" :list="langs" valueItem="value" textItem="name" v-model="lang"/>
        </div>
        <img src=".././assets/img/swen.png" alt="" class="w-full h-[44px]">
    </header>
</template>
<script>
import Select from './selects/default.vue'
export default {
    name: 'HeaderComponent',
    components: {
        Select
    },
    data() {
        return {
            langs: [
                {
                    id: 1,
                    name: 'RU',
                    value: 'ru'
                },
                {
                    id: 2,
                    name: 'EN',
                    value: 'en'
                }
            ],
            lang: 'en'
        }
    }
}
</script>