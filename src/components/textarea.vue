<template>
    <textarea  :value="modelValue" @input="$emit('update:modelValue', $event.target.value)"
    :rows="rows" class="p-5 outline-none w-full" :placeholder="placeholder"></textarea>
</template>
<script>
export default {
    name: 'TextAreaComponent',
    props: {
        modelValue: {},
        rows: {
            type: Number,
            default: 3
        },
        placeholder: {
            type: String
        }
    }
}
</script>