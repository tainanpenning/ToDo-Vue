<script setup>
    const props = defineProps(["adicionaTarefa", "tarefaTemp", "trocarFiltro", "editaTarefaTemp"])
</script>

<template>
    <form @submit.prevent="props.adicionaTarefa">
        <div class="row">
            <div class="col">
                <input required class="form-control" type="text" placeholder="Digite a descrição da tarefa"
                    :value="props.tarefaTemp" @change="props.editaTarefaTemp">
            </div>
            <div class="col-md-2">
                <button class="btn btn-primary" type="submit">Adicionar</button>
            </div>
            <div class="col-md-2">
                <select class="form-control text-center" @change="props.trocarFiltro">
                    <option value="todas">Todas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>

<style scoped>
    @media screen and (max-width: 767px) {
        button{
            margin: 8px 0;
            width: 100%;
        }
    }
</style>