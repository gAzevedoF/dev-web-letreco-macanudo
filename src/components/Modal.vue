<script setup>
import { defineProps } from "vue";

const props = defineProps({
    terminouAsTentativas: {
        type: Boolean,
        default: true
    },
    
    descobriuAPalavra: {
        type: Boolean,
        default: true
    },
})
</script>

<template>
      <div
        v-show="terminouAsTentativas"
        class="
          absolute
          inset-0
          flex
          items-center
          justify-center
          bg-gray-700 bg-opacity-50
        "
      >
        <div class="max-w-2xl p-6 mx-4 bg-white rounded-md shadow-xl">
          <div class="flex items-center justify-between">
            <h3 v-if="descobriuAPalavra" class="text-2xl">Tri afú</h3>
            <h3 v-else class="text-2xl">É de cair os butiá do bolso</h3>
          </div>
          <div class="mt-4">
            <img v-if="descobriuAPalavra" src="https://c.tenor.com/aHiJ8y20QToAAAAM/o-cris-pereira-good.gif" alt="">
            <img v-else src="https://c.tenor.com/nuE08aCbPHYAAAAC/mas-que-barbaridade.gif" alt="">
          </div>
        </div>
      </div>
</template>
