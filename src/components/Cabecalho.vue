<script setup>
    const props = defineProps(['tarefasPendentes'])
</script>
<template>
    <header class="p-5 my-4 bg-light">
        <h1>Minhas tarefas</h1>
        <p>
            Você possui <strong>{{ props.tarefasPendentes}}</strong> tarefas pendentes.
        </p>
    </header>
</template>