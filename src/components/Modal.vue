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
            <h3 class="text-2xl">Model Title</h3>
          </div>
          <div class="mt-4">
            <p v-if="descobriuAPalavra" class="mb-4 text-sm">
              Parabéns
            </p>
            <p v-else class="mb-4 text-sm">
              Veash
            </p>
          </div>
        </div>
      </div>
</template>
