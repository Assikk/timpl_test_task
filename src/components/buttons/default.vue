<template>
    <button class="flex items-center justify-center gap-2.5 bg-[#0F0A2F] rounded-[40px] text-white font-medium py-2.5"
    :class="[
    {'light': light}
    ]">
        <slot name="prev-icon"/>
        <slot/>
        <slot name="next-icon"/>
    </button>
</template>
<script>
export default {
    name: 'DefaultButtonComponent',
    props: {
        light: {
            type: Boolean,
            default: false
        }
    }
}
</script>
<style scoped>
.light {
    background: #9771FD;
}
</style>