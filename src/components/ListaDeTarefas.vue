<script setup>
 const props = defineProps(['tarefas'])
</script>
<template>
    <ul class="list-group mt-4" v-if="props.tarefas.length">
        <li class="list-group-item" v-for="tarefa in props.tarefas">
                <input 
                @change="evento => tarefa.finalizada = evento.target.checked" 
                :checked="tarefa.finalizada" 
                :id="tarefa.descricao" 
                type="checkbox"
            >
            <label 
            :for="tarefa.descricao" 
            class="ms-3" 
            :class="{done: tarefa.finalizada}"
            >
            {{ tarefa.descricao }}
            </label>
        </li>
    </ul>
    <p class="mt-4" v-else>Nenhuma tarefa para exibir.</p>
</template>
<style scoped>
    .done {
        text-decoration: line-through;
    }
</style>
