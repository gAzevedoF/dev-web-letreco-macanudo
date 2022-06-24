<script setup>
import { defineProps, ref, watch } from "vue";
import Letra from "./Letra.vue"


const props = defineProps({
    tentativa: String,
    palavraDaRodada: String,
    tentativaFinalizada: Boolean
})

const corPorLetra = ref(["", "", "", "", "", ""]);

watch(
  () =>  {
    if (props.tentativaFinalizada) {
      let palavraDaRodada = props.palavraDaRodada;
      let palavraDaTentativa = props.tentativa;
      let coresLetra = [];

      for (let i = 0; i < palavraDaRodada.length; i++) {
        coresLetra.push("red")
      }

      for (let i = 0; i < palavraDaRodada.length; i++) {
        if (palavraDaRodada.charAt(i) == palavraDaTentativa.charAt(i)) {
          coresLetra[i] = "green";
        } else {
           for (let j = 0; j < palavraDaRodada.length; j++) {
                 if (palavraDaRodada.charAt(j) == palavraDaTentativa.charAt(i)) {
                  coresLetra[i] = "yellow";
                }
            }
           }

      }
      corPorLetra.value = coresLetra;
    }
  }
); 

</script>

<template>
  <div class="grid max-w-screen-sm gap-1 mx-auto mb-1"
  :class="{
    'grid-cols-3': palavraDaRodada.length == 3,
    'grid-cols-4': palavraDaRodada.length == 4,
    'grid-cols-5': palavraDaRodada.length == 5,
    'grid-cols-6': palavraDaRodada.length == 6,
    'grid-cols-7': palavraDaRodada.length == 7,
    'grid-cols-8': palavraDaRodada.length == 8,
    'grid-cols-9': palavraDaRodada.length == 9,
  
  }">
    <Letra
        v-for="i in props.palavraDaRodada.length"
        :key="i"
        :letra="tentativa[i-1]"
        :corDaLetra="corPorLetra[i-1]"
    />
  </div>
</template>

<style>

</style>