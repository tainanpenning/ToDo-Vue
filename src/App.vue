<script setup>
import { reactive } from 'vue';

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
                finalizada: false,
            },
            {
                titulo: "Ir para a academia",
                finalizada: true,
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
        <header class="p-5 mb-4 mt-4 bg-light rounded-3">
            <h1>Minhas Tarefas</h1>
            <p v-if="getTarefasPendentes().length > 0">
                Você possui {{ getTarefasPendentes().length }} tarefas pendentes
            </p>
            <p v-if="getTarefasPendentes().length === 0">
                Você não possui tarefas pendentes
            </p>
        </header>
        <form @submit.prevent="adicionaTarefa">
            <div class="row">
                <div class="col">
                    <input required class="form-control" type="text" placeholder="Digite a descrição da tarefa" :value="estado.tarefaTemp" @change="e => estado.tarefaTemp = e.target.value">
                </div>
                <div class="col-md-2">
                    <button class="btn btn-primary" type="submit">Adicionar</button>
                </div>
                <div class="col-md-2">
                    <select class="form-control" @change="e => estado.filtro = e.target.value">
                        <option value="todas">Todas</option>
                        <option value="pendentes">Pendentes</option>
                        <option value="finalizadas">Finalizadas</option>
                    </select>
                </div>
            </div>
        </form>
        <ul class="list-group mt-4">
            <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
                <input type="checkbox" @change="e => tarefa.finalizada = e.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo">
                <label class="ms-3" :class="{ done: tarefa.finalizada }" :for="tarefa.titulo">
                    {{ tarefa.titulo }}
                </label>
            </li>
        </ul>
    </div>
</template>

<style scoped>
    .done{
        text-decoration: line-through;
    }
</style>
