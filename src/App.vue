<template>
  <main class="columns is-gapless is-multiline " :class="{'modo-escuro': modoEscuroAtivo}">
    <div class="column is-one-fifth">
      <BarraLateral @aoTemaAlterado="trocarTema"/>
    </div>
    <div class="column is-three-fifth conteudo">
      <Formulario @aoSalvarTarefa="salvarTarefa"/>
      <div class="lista">
        <Tarefa v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa"/>
        <box v-if="listaVazia">
          Você não está muito produtivo hoje :(
        </box>
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from '@/components/BarraLateral.vue';
import Formulario from '@/components/Formulario.vue';
import Tarefa from '@/components/Tarefa.vue'
import ITarefa from '@/interfaces/ITarefa'
import Box from '@/components/Box.vue'

export default defineComponent({
  name: 'App',
  components: {
    BarraLateral,
    Formulario,
    Tarefa,
    Box,
  }, 

  data () {
    return {
      tarefas: [] as ITarefa[],
      modoEscuroAtivo: false,
    }
  },

  computed: {
    listaVazia () : boolean {
      return this.tarefas.length === 0
    }
  },

  methods: {
    salvarTarefa (tarefa: ITarefa) {
      this.tarefas.push(tarefa)
    },
    trocarTema (modoEscuroAtivo : boolean) {
      this.modoEscuroAtivo = modoEscuroAtivo
    },
  }
});
</script>

<style>
.lista {
  padding: 1em;
}

main {
  --bg-primario: #fff;
  --txt-primario: #000;
}

main.modo-escuro {
  --bg-primario: #2b2d42;
  --txt-primario: #ddd;
}

.conteudo {
  background-color: var(--bg-primario);
}
</style>
