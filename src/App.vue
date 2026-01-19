<script setup>
import { reactive } from 'vue';

const estados = reactive({
  filtro: "todas",
  tarefaTamps: "",
  tarefas: [
    {
      titulo: "Estudar ES6",
      finalizada: false
    },
    {
      titulo: "Estudar SCSS",
      finalizada: false
    },
    {
      titulo: "treinar",
      finalizada: true
    }
  ]
})

const getTarefasPendente = () => {
  return estados.tarefas.filter(tarefa => !tarefa.finalizada)
}
const getTarefasFinalizadas = () => {
  return estados.tarefas.filter(tarefa => tarefa.finalizada)
}


const getTaredasFiltradas = () => {
  const {filtro} = estados

  switch(filtro){
    case 'pendentes':
      return getTarefasPendente()
    case "finalizadas":
      return getTarefasFinalizadas()
    default:
      return estados.tarefas
  }
}

const cadastroTarefa= (e) => {
  const tarefaNova = {
    titulo: estados.tarefaTamps,
    finalizada: false
  }
  estados.tarefas.push(tarefaNova)
  estados.tarefaTamps = ""
}

</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>Você possui {{ getTarefasPendente().length }} tarefas pendentes</p>
    </header>
    <form @submit.prevent="cadastroTarefa" action="">
      <div class="row">
        <div class="col">
          <input @change="evento => estados.tarefaTamps = evento.target.value" required="" type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div @change="evento => estados.filtro = evento.target.value" class="col-md-2">
          <select class="form-control">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas"> Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTaredasFiltradas()">
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">{{ tarefa.titulo }}</label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
