<script setup>
import { defineProps } from "vue";
import Parabens from './assets/o-cris-pereira-good.gif';
import GameOver from './assets/mas-que-barbaridade.gif';

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
            <img v-if="descobriuAPalavra" :src="Parabens" alt="">
            <img v-else :src="GameOver" alt="">
          </div>
        </div>
      </div>
</template>
