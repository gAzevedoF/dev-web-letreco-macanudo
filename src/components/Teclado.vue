<template>
    <div class="simple-keyboard"></div>
</template>

<script setup>

import { onMounted, defineEmits, ref } from "vue"
import Teclado from "simple-keyboard"
import "simple-keyboard/build/css/index.css"

const teclado = ref(null)

onMounted(() => {
    teclado.value = new Teclado({
        onKeyPress: tecla => onTeclaPressionada(tecla),
        layout: {
            default: [
            "q w e r t y u i o p",
            "a s d f g h j k l",
            "z x c v b n m {bksp} {enter}",
            ],
        },
        display: {
        "{enter}": "↵",
        "{bksp}": "⌫",
    }
    });
})

const emit = defineEmits(["onTeclaPressionada"]);

function onTeclaPressionada(tecla) {
  emit("onTeclaPressionada", tecla)
}

</script>

<style>

</style>