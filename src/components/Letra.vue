<script setup>
import { defineProps } from "vue";


const props = defineProps({
    letra: {
        type: String,
        default: ""
    },
    
    corDaLetra: {
        type: String,
        default: "",
    },
})

</script>

<template>
    <div class="col-span-1 flex items-center justify-center h-16 uppercase border-2" 
    :class="{
      'border-red-700 bg-red-700 text-white': corDaLetra == 'red',
      'border-green-600 bg-green-600 text-white': corDaLetra == 'green',
      'border-yellow-500 bg-yellow-500 text-white': corDaLetra == 'yellow',
    }"
    >
        <span v-text="letra"></span>
    </div>    
</template>

<style>

</style>