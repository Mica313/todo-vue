<script setup>
import {reactive} from 'vue';
  const estado = reactive({
    filtro:'todas',
    tarefaTemp:'',
    tarefas:[
      {
        titulo:'estudar ES6',
        finalizda:false,
      },
      {
        titulo:'estudar sass',
        finalizda:false,
      },
      {
        titulo:'ir para academia',
        finalizda:true,
      }
    ]
  })
  const gettarefasP = () =>{
    return estado.tarefas.filter(tarefa => !tarefa.finalizda)
  }
  const gettarefasFinalizadas = () =>{
    return estado.tarefas.filter(tarefa => tarefa.finalizda)
  }
  const gettarefasFiltradas = () => {
    const {filtro} = estado;
    switch(filtro){
      case 'pendentes':return gettarefasP();
      case 'finalizadas':return gettarefasFinalizadas();
      default:return estado.tarefas;
    }
  }
  const cadastrarTarefa = ()=>{
    const tarefaNova = {
      titulo:estado.tarefaTemp,
      finalizda:false
    }
    estado.tarefas.push(tarefaNova);
    estado.tarefaTemp = '';
  }
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>Voce possui {{ gettarefasP().length }} tarefas pendentes</p>
    </header>
    <form @submit.prevent="cadastrarTarefa">
    <div class="row">
      <div class="col">
        <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required type="text" class="form-control" placeholder="digite a descrição da tarefa">
      </div>
      <div class="col-md-2">
        <button type="submit" class="btn btn-primary">cadastrar tarefa</button>
      </div>
      <div class="col-md-2">
        <select @change="evento => estado.filtro = evento.target.value" class="form-control">
          <option value="todas">Todas</option>
          <option value="pendentes">pendentes</option>
          <option value="finalizadas">finalizadas</option>
        </select>
      </div>
    </div>
  </form>
  <ul class="list-group mt-4">
    <li class="list-group item" v-for="tarefa in gettarefasFiltradas()">
      <input @change="evento => tarefa.finalizda = evento.target.checked" :checked="tarefa.finalizda" :id="tarefa.titulo" type="checkbox">
      <label :class="{done: tarefa.finalizda === true}" class="ms-3" :for="tarefa.titulo">{{ tarefa.titulo }}</label>
    </li>
  </ul>
  </div>
</template>

<style scoped>
  .done{
    text-decoration:line-through;
  }
</style>
