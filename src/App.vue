<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';

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
      titulo: "Treinar",
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
  const { filtro } = estados
  switch (filtro) {
    case 'pendentes':
      return getTarefasPendente()
    case "finalizadas":
      return getTarefasFinalizadas()
    default:
      return estados.tarefas
  }
}

const cadastroTarefa = (e) => {
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
    <Cabecalho :tarefas-pendentes="getTarefasPendente().length" />
    <Formulario :trocar-filtro="evento => estados.filtro = evento.target.value" :tarefa-tamps="estados.tarefaTamps"
      :edita-tarefa-temp="evento => estados.tarefaTamps = evento.target.value" :cadastro-tarefa="cadastroTarefa" />
    <ListaDeTarefas :tarefas="getTaredasFiltradas()"/>
  </div>
</template>


