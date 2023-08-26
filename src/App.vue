<script setup>
  import {reactive} from 'vue';
  import Header from './components/Header.vue';
  import Form from './components/Form.vue';
  import Lista from './components/Lista.vue';
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
    <Header :tarefas-pendentes="gettarefasP.length"></Header>
    <Form :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :editatarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastrarTarefa()"></Form>
    <Lista :tarefas="gettarefasFiltradas()"></Lista>
    
  </div>
</template>
