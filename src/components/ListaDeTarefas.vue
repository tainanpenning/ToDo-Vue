<script setup>
    const props = defineProps(["tarefas", "estado"])
</script>

<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefas">
            <input type="checkbox" @change="e => tarefa.finalizada = e.target.checked" :checked="tarefa.finalizada"
                :id="tarefa.titulo">
            <label class="ms-3" :class="{ done: tarefa.finalizada }" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
        <p class="p-2 list-group-item text-center" v-if="props.tarefas.length === 0">Sem tarefas {{ props.estado.filtro }}</p>
    </ul>
</template>

<style scoped>
    .done{
        text-decoration: line-through;
    }
</style>