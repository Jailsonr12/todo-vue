<script setup>
    const props = defineProps(['cadastroTarefa', 'tarefaTamps', 'trocarFiltro', "editaTarefaTemp"])
</script>


<template>
    <form @submit.prevent="props.cadastroTarefa" action="">
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTamps" @change="props.editaTarefaTemp"  required="" type="text"
                    placeholder="Digite aqui a descrição da tarefa" class="form-control">
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div @change="props.trocarFiltro" class="col-md-2">
                <select class="form-control">
                    <option value="todas">Todas tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas"> Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>