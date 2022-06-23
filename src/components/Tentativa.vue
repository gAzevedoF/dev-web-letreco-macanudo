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
  :class="'grid-cols-'+palavraDaRodada.length">
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