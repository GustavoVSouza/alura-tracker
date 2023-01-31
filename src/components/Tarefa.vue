<template>
 <Box>
    <div class="columns">
        <div class="column is-7">
            {{ tarefa.descricao || 'Tarefa sem descrição'}}
        </div>
        <div class="column">
            <Contador :tempoEmSegundos="tarefa.duracaoEmSegundos"/>
        </div>
    </div>
 </Box> 
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';
import Contador from "@/components/Contador.vue";
import ITarefa from '@/interfaces/ITarefa';
import Box from './Box.vue';

export default defineComponent ({
    name: 'Tarefa', 
    components: {
        Contador,
        Box,
    },
    props: {
        tarefa: {
            type: Object as PropType<ITarefa>,
            required: true
        }
    }
})
</script>

<style scoped>
    
</style>