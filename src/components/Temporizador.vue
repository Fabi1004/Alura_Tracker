<template>
  <div class="is-flex is-align-items-center is-justify-content-space-between">
    <Cronometro
      :tempoEmSegundos="tempoEmSegundos"
      :disabled="cronometroRodando"
    />
    <button class="button" @click="iniciar()" :disabled="cronometroRodando">
      <span class="icon">
        <i class="fas fa-play"></i>
      </span>
      <span>play</span>
    </button>
    <button class="button" @click="parar()" :disabled="!cronometroRodando">
      <span class="icon">
        <i class="fas fa-stop"></i>
      </span>
      <span>stop</span>
    </button>
    <button class="button" @click="finalizar()" :disabled="!cronometroRodando">
      <span class="icon">
        <i class="fas fa-step-forward"></i>
      </span>
      <span>End</span>
    </button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

import Cronometro from "./Cronometro.vue";

export default defineComponent({
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Temporizador",
  emits: ["aoTemporizadorFinalizado"],
  components: {
    Cronometro,
  },

  data() {
    return {
      tempoEmSegundos: 0,
      cronometro: 0,
      cronometroRodando: false,
    };
  },

  methods: {
    iniciar() {
      // começar a contagem
      this.cronometroRodando = true;
      this.cronometro = setInterval(() => {
        this.tempoEmSegundos += 1;
      }, 1000);
    },
    parar() {
      this.cronometroRodando = false;
      clearInterval(this.cronometro);
    },

    finalizar() {
      this.cronometroRodando = false;
      clearInterval(this.cronometro);
      this.$emit("aoTemporizadorFinalizado", this.tempoEmSegundos);
      this.tempoEmSegundos = 0;
    },
  },
});
</script>

<style>
.button {
  margin: 0 3px;
}
</style>
