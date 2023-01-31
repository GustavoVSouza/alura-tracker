<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
        <Contador :tempoEmSegundos="tempoEmSegundos" />
        <button class="button" @click="iniciar" :disabled="cronometroRodando">
            <span class="icon">
                <i class="fas fa-play"></i>
            </span>
            <span>play</span>
        </button>
        <button class="button" @click="finalizar" :disabled="!cronometroRodando">
            <span class="icon">
                <i class="fas fa-stop"></i>
            </span>
            <span>stop</span>
        </button>
    </div>
</template>

<script lang="ts">
import { defineComponent } from "vue"
import Contador from '@/components/Contador.vue'

export default defineComponent({
    name: "Temporizador",
    emits: ['aoTemporizadorFinalizado'],
    components: {
        Contador
    },
    data () {
        return {
            tempoEmSegundos: 0,
            Contador: 0,
            cronometroRodando: false,
        }
    },
    methods: {
        iniciar () {
            this.cronometroRodando = true
            this.Contador = setInterval(() => {
                this.tempoEmSegundos += 1
            }, 200)
        },
        finalizar () {
            this.cronometroRodando = false
            clearInterval(this.Contador)
            this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
            this.tempoEmSegundos = 0
        }
    }
})
</script>