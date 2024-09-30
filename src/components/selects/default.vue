<template>
    <select :id="id" :value="modelValue" @input="$emit('update:modelValue', $event.target.value)" class="outline-none min-w-[50px]">
        <option v-for="item in list" :key="item.id" :value="item[valueItem]">{{item[textItem]}}</option>
    </select>
</template>
<script>
import Arrow from '/arrow-down.svg'
export default {
    name: 'DefaultSelectComponent',
    props: {
        id: {
            type: String,
            required: true
        },
        list: {
            type: Array,
            required: true
        },
        valueItem: {
            type: String,
            required: true
        },
        textItem: {
            type: String,
            required: true
        },
        modelValue: {}
    },
    methods: {
    changeStyles() {
      let select = document.getElementById(this.id)
      select.style.webkitAppearance = 'none'
      select.style.background = `url(${Arrow}) 95% 50% no-repeat`
    }
  },
  mounted() {
    this.changeStyles()
  }
}
</script>