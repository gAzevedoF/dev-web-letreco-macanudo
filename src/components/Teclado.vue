<template>
  <div class="simple-keyboard"></div>
</template>

<script setup>
import { onMounted, defineEmits, ref, watch } from "vue";
import Teclado from "simple-keyboard";
import "simple-keyboard/build/css/index.css";

const props = defineProps({
  letrasJogadas: Object
});

const teclado = ref(null);

onMounted(() => {
  teclado.value = new Teclado({
    onKeyPress: tecla => onTeclaPressionada(tecla),
    layout: {
      default: [
        "q w e r t y u i o p",
        "a s d f g h j k l",
        "z x c v b n m {bksp} {enter}"
      ]
    },
    display: {
      "{enter}": "↵",
      "{bksp}": "⌫"
    }
  });
});

watch(
  () => props.letrasJogadas,
  letrasJogadas => {
    teclado.value.addButtonTheme(props.letrasJogadas.certo.join(" "), "certo");
    teclado.value.addButtonTheme(props.letrasJogadas.quase.join(" "), "quase");
    teclado.value.addButtonTheme(props.letrasJogadas.errou.join(" "), "errou");
  },
  { deep: true }
);

const emit = defineEmits(["onTeclaPressionada"]);

function onTeclaPressionada(tecla) {
  emit("onTeclaPressionada", tecla);
}
</script>

<style>
div.errou {
  @apply bg-red-700 !important;
  @apply text-white;
}
div.certo {
  @apply bg-green-600 !important;
  @apply text-white;
}
div.quase:not(.certo) {
  @apply bg-yellow-500 !important;
  @apply text-white;
}
</style>