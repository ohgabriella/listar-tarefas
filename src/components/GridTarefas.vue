<template>
  <div class="lista">
    <template v-if="tarefas.length">
      <Tarefa class="grid-lista" 
      v-for="(tarefa, i) in tarefas" :key="tarefa.name" 
      @deletarTarefa="$emit('deletarTarefa', i)"
      @changeStatus="$emit('changeStatus', i)"
      :tarefa="tarefa"></Tarefa>
    </template>
    <p v-else class="no-lista">Sua vida está em dia :)</p>
  </div>
</template>

<script>
import Tarefa from "./Tarefa";

export default {
    components: { Tarefa },
    props: {
        tarefas: { type: Array, required: true}
    }
};
</script>

<style scoped>

.lista {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}

.grid-lista {
  margin: 10px;
}

.no-lista {
  color: #aaa;
  font-size: 1.7rem;
}
</style>