<script setup>
    const props = defineProps(['cadastraTarefa', 'tarefaTemp', 'trocarFiltro', 'editatarefaTemp']);
</script>
<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTemp" @change="props.editatarefaTemp" required
                    type="text" class="form-control" placeholder="digite a descrição da tarefa">
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">cadastrar tarefa</button>
            </div>
            <div class="col-md-2">
                <select @change="props.trocarFiltro" class="form-control">
                    <option value="todas">Todas</option>
                    <option value="pendentes">pendentes</option>
                    <option value="finalizadas">finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>