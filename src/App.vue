<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup

import Tentativa from "./components/Tentativa.vue";
import Teclado from "./components/Teclado.vue";
import Modal from "./components/Modal.vue";
import Logo from "./assets/logo.png";
import { reactive } from "vue";

const palavrasDificuldadeFacil = [
  "bah",
  "tri",
  "xis",
  "tche",
  "boia",
  "mate",
  "pila"
];

const palavrasDificuldadeMedia = [
  "butia",
  "chiar",
  "rengo",
  "taipa",
  "bucha",
  "chapa",
  "cusco",
  "bueno",
  "china",
  "arriar",
  "prenda",
  "trovar",
  "pousar",
  "peleia"
];

const palavrasDificuldadeDificil = [
  "pechada",
  "vivente",
  "chavear",
  "entonces",
  "guaiaca",
  "minuano",
  "guaipeca",
  "talagaço",
  "reinento",
  "entonces",
  "macanudo",
  "manotaço",
  "arreganho",
  "atucanado",
  "bergamota",
  "cacetinho",
  "lagartear",
  "querencia"
];

const palavras = [
  palavrasDificuldadeFacil,
  palavrasDificuldadeMedia,
  palavrasDificuldadeDificil
];

const estadoAtual = reactive({
  palavraDaRodada: "",
  tentativas: ["", "", "", "", "", ""],
  tentativaJogada: 0,
  descobriuAPalavra: false,
  terminouAsTentativas: false,
  dificuldade: 0,
  letrasJogadas: {
    certo: [],
    quase: [],
    errou: []
  }
});

const teclaPressionada = tecla => {
  const tentativaAtual = estadoAtual.tentativas[estadoAtual.tentativaJogada];
  const palavraDaRodada = estadoAtual.palavraDaRodada;

  if (
    tecla == "{enter}" &&
    tentativaAtual.length == palavraDaRodada.length &&
    palavraExistente(tentativaAtual)
  ) {
    estadoAtual.tentativaJogada++;

    checaLetrasJogadas(tentativaAtual);

    if (tentativaAtual == palavraDaRodada) {
      estadoAtual.terminouAsTentativas = true;
      estadoAtual.descobriuAPalavra = true;
      return;
    }

    if (estadoAtual.tentativaJogada == 6) {
      estadoAtual.terminouAsTentativas = true;
      estadoAtual.descobriuAPalavra = tentativaAtual == palavraDaRodada;
      return;
    }
  } else if (tecla == "{bksp}") {
    estadoAtual.tentativas[estadoAtual.tentativaJogada] = tentativaAtual.slice(0, -1);
  } else {
    if (tecla != "{enter}") {
      estadoAtual.tentativas[estadoAtual.tentativaJogada] += tecla;
    }
  }
};

let selecionaDificuldade = dificuldadeSelecionada => {
  estadoAtual.dificuldade = dificuldadeSelecionada;
  let palavrasParaDificuldade = palavras[dificuldadeSelecionada - 1];
  let palavra = palavrasParaDificuldade[Math.ceil(Math.random() * palavrasParaDificuldade.length)].toLowerCase();
  estadoAtual.palavraDaRodada = palavra;
};

let palavraExistente = palavraTentativa => {
  let indice = estadoAtual.dificuldade - 1;

  let palavrasDaPartida = palavras[indice];

  return palavrasDaPartida.includes(palavraTentativa);
};

let checaLetrasJogadas = palavraTentativa => {
  let palavraRodada = estadoAtual.palavraDaRodada;

  for (let i = 0; i < palavraRodada.length; i++) {
    let letraTentativa = palavraTentativa.charAt(i);
    if (palavraRodada.charAt(i) == letraTentativa) {
      estadoAtual.letrasJogadas.certo.push(letraTentativa);
    } else {
      if (palavraRodada.includes(letraTentativa)) {
        estadoAtual.letrasJogadas.quase.push(letraTentativa);
      } else {
        estadoAtual.letrasJogadas.errou.push(letraTentativa);
      }
    }
  }
};
</script>

<template>
  <div>
    <header 
      class="h-36 bg-gradient-to-r from-green-500 via-red-700 to-yellow-500 flex-shrink-0 flex items-center justify-center"
    >
      <img class="w-24" :src="Logo" alt />
      <p class="font-mono text-white sm:text-4xl lg:text-6xl">LETRECO MACANUDO</p>
    </header >

    <div class="min-h-screen"
      v-if="estadoAtual.dificuldade == 0"
    >
      <div class="mt-16 bg-gradient-to-r p-[6px] from-green-500 via-red-700 to-yellow-500 max-w-md mx-auto rounded-lg">

        <div class="flex flex-col space-y-4 items-center bg-white text-white rounded-lg p-4">
        <p class="font-semibold text-2xl dark:text-white uppercase text-gray-700">Seleciona a dificuldade vivente</p>
        <button
          v-on:click="selecionaDificuldade(1)"
          class="w-24 bg-transparent hover:bg-green-500 text-green-700 font-semibold hover:text-white py-2 px-4 border border-green-500 hover:border-transparent rounded"
        >Piá</button>

        <button
          v-on:click="selecionaDificuldade(2)"
          class="w-24 bg-transparent hover:bg-yellow-500 text-yellow-700 font-semibold hover:text-white py-2 px-4 border border-yellow-500 hover:border-transparent rounded"
        >Rapaz</button>

        <button
          v-on:click="selecionaDificuldade(3)"
          class="w-24 bg-transparent hover:bg-red-500 text-red-700 font-semibold hover:text-white py-2 px-4 border border-red-500 hover:border-transparent rounded"
        >Veterano</button>
        </div>
      </div>
    </div>
    <div v-else class="flex flex-col h-screen min-h-screen max-w-md mx-auto justify-evenly">
      <div>
        <Tentativa
          v-for="(tentativa, i) in estadoAtual.tentativas"
          :key="i"
          :tentativa="tentativa"
          :palavraDaRodada="estadoAtual.palavraDaRodada"
          :tentativaFinalizada="i < estadoAtual.tentativaJogada"
        />
      </div>

      <Teclado :letrasJogadas="estadoAtual.letrasJogadas" @onTeclaPressionada="teclaPressionada" />

      <Modal
        v-bind:terminouAsTentativas="estadoAtual.terminouAsTentativas"
        :descobriuAPalavra="estadoAtual.descobriuAPalavra"
      />
    </div>

    <footer class="bg-gray-400 text-center lg:text-left">
      <div class="text-gray-700 text-center p-4">
        © 2022 Copyright:
    <a class="text-gray-800" href="https://www.linkedin.com/in/guilherme-ferreira-099a681b4">Guilherme Ferreira</a>
  </div>
</footer>
  </div>
</template>


<style>
</style>
