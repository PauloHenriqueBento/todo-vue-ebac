<script setup>
import {reactive} from 'vue'
const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [
    {descricao: 'Estudar', finalizada: false},
    {descricao: 'Ler', finalizada: false },
    {descricao: 'Academia', finalizada: true },
  ]
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
}

const getTarefasFiltradas = () => {
  const { filtro } = estado;

  switch (filtro) {
    case 'pendentes':
      return getTarefasPendentes();
    case 'finalizadas':
      return getTarefasFinalizadas();
    default:
      return estado.tarefas
  }
}

const cadastraTarefa = () => {  
  const tarefaNova = {
    descricao: estado.tarefaTemp,
    finalizada: false
  }
  estado.tarefas.push(tarefaNova);
  estado.tarefaTemp = ''
}

</script>

<template>
  <div class="container">
    <header class="p-5 my-4 bg-light">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui <strong>{{ getTarefasPendentes().length }}</strong> tarefas pendentes.
      </p>
    </header>
    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input 
            required 
            @change="evento => estado.tarefaTemp = evento.target.value" 
            :value="estado.tarefaTemp"
            type="text" 
            placeholder="Digite aqui a descrição da tarefa" 
            class="form-control" 
          />
        </div>
        <div class="col-md-2">
          <button class="btn btn-primary" type="submit">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select class="form-control" @change="evento => estado.filtro = evento.target.value">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
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
  </div>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
