<script setup>
    import { reactive } from 'vue';
    import Cabecalho from './components/Cabecalho.vue';
    import Formulario from './components/Formulario.vue';
    import ListaDeTarefas from './components/ListaDeTarefas.vue';

    const estado = reactive({
        filtro: "todas",
        tarefaTemp: "",
        tarefas: [
            {
                titulo: "Estudar ES6",
                finalizada: false,
            },
            {
                titulo: "Estudar SASS",
                finalizada: true,
            },
            {
                titulo: "Estudar VueJS",
                finalizada: false,
            },
        ]
    })

    const getTarefasPendentes = () => {
        return estado.tarefas.filter(tarefa => !tarefa.finalizada)
    }
    
    const getTarefasFinalizadas = () => {
        return estado.tarefas.filter(tarefa => tarefa.finalizada)
    }

    const getTarefasFiltradas = () => {
        const { filtro } = estado

        switch (filtro){
            case "pendentes":
                return getTarefasPendentes()
            case "finalizadas":
                return getTarefasFinalizadas()
            default:
                return estado.tarefas
        }
    }

    const adicionaTarefa = () => {
        const novaTarefa = {
            titulo: estado.tarefaTemp,
            finalizada: false,
        }
        estado.tarefas.push(novaTarefa)
        estado.tarefaTemp = ""
    }
</script>

<template>
    <div class="container">
        <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"></Cabecalho>
        <Formulario :trocar-filtro="e => estado.filtro = e.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="e => estado.tarefaTemp = e.target.value" :adiciona-tarefa="adicionaTarefa"></Formulario>
        <ListaDeTarefas :tarefas="getTarefasFiltradas()" :estado="estado"></ListaDeTarefas>
    </div>
</template>

<style scoped>
    @media screen and (min-width: 1023px) {
        .container{
            max-width: 960px;
        }
    }
</style>