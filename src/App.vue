<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup

import Tentativa from "./components/Tentativa.vue"
import Teclado from './components/Teclado.vue'
import Modal from './components/Modal.vue'
import { reactive, onMounted } from "vue"

const palavras = [
  "Arreganho",
  "Arriar",
  "Atucanado",
  "Bah",
  "Tche",
  "Bergamota",
  "Cacetinho",
  "butia",
  "Gringo",
  "Guaipeca",
  "Lagartear",
  "Pechada",
  "Prenda",
  "Rengo",
  "Taipa",
  "Tri",
  "Trovar",
  "Vivente",
  "Talagaço",
  "Bucha",
  "Reinento",
  "Chavear",
  "Pousar",
  "Chapa",
  "Boia"
]

const estadoAtual = reactive({
  palavraDaRodada:  palavras[Math.ceil(Math.random()*palavras.length)].toLowerCase(),
  tentativas: ["", "", "", "", "", ""],
  quantidadeTentativas: 0,
  descobriuAPalavra: false,
  terminouAsTentativas: false,
})

const handleInput = (tecla) => {

  const tentativaAtual = estadoAtual.tentativas[estadoAtual.quantidadeTentativas]
  const palavraDaRodada = estadoAtual.palavraDaRodada
  console.log(palavraDaRodada)

  if(tecla == "{enter}" && tentativaAtual.length == palavraDaRodada.length) {
    estadoAtual.quantidadeTentativas++;

    if(tentativaAtual == palavraDaRodada){
    estadoAtual.terminouAsTentativas = true;
    estadoAtual.descobriuAPalavra = true;
    return
  }

    if(estadoAtual.quantidadeTentativas == 6) {
    estadoAtual.terminouAsTentativas = true
    estadoAtual.descobriuAPalavra = (tentativaAtual == palavraDaRodada)
    return
  }
  
  } else if(tecla == "{bksp}") {
    estadoAtual.tentativas[estadoAtual.quantidadeTentativas] = tentativaAtual.slice(0, -1);
  
  } else {
      estadoAtual.tentativas[estadoAtual.quantidadeTentativas] += tecla;
    }
}


</script>

<template>
  <div>
    <div class="h-36 bg-gradient-to-r from-green-500 via-red-500 to-yellow-500 flex-shrink-0 flex items-center justify-center">
      <img class="w-full h-36 sm:h-auto object-cover sm:w-36 rounded-t-lg md:rounded-none md:rounded-l-lg" src="src\assets\logo.png" alt="">
      <p class="font-mono text-white sm:text-4xl lg:text-6xl">MACANUDO</p>
    </div>
    
    <div class="flex flex-col h-screen max-w-md mx-auto justify-evenly">

      <div>
        <Tentativa
          v-for="(tentativa, i) in estadoAtual.tentativas"
          :key="i"
          :tentativa="tentativa"
          :palavraDaRodada="estadoAtual.palavraDaRodada"
          :tentativaFinalizada="i < estadoAtual.quantidadeTentativas"
        />
      </div>

      <Teclado @onTeclaPressionada="handleInput"/> 

      <Modal 
        :terminouAsTentativas="estadoAtual.terminouAsTentativas" 
        :descobriuAPalavra="estadoAtual.descobriuAPalavra" 
      />
        
      
    </div>

    <div class="bg-gray-500 h-36 flex items-center justify-center">
      <p class="font-mono text-1xl">Desenvolvimento para Web/2022</p>
    </div>

    

  </div>
</template>


<style>

</style>
