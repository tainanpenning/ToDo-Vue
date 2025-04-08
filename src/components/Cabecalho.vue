<script setup>
    const props = defineProps(["tarefasPendentes"])
</script>

<template>
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
        <h1>Minhas Tarefas</h1>
        <p v-if="props.tarefasPendentes > 0">
            Você possui {{ props.tarefasPendentes }} tarefas pendentes
        </p>
        <p v-if="props.tarefasPendentes === 0">
            Você não possui tarefas pendentes
        </p>
    </header>
</template>

<style scoped>
    @media screen and (max-width: 767px) {
        header{
            text-align: center;
        }
    }
</style>