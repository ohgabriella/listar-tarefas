<template>
  <div id="app">
    <h1>Tarefas</h1>
    <NovaTarefa @tarefaAdicionada="addTarefa"></NovaTarefa>
    <GridTarefas @deletarTarefa="tarefaDeletada" @changeStatus="statusChange" :tarefas="tarefas" />
  </div>
</template>

<script>
import NovaTarefa from "./components/NovaTarefa";
import GridTarefas from "./components/GridTarefas";

export default {
  components: { NovaTarefa, GridTarefas },
  data() {
    return {
      tarefas: [
      ]
    };
  },
  methods: {
    addTarefa(tarefa) {
      const sameName = t => t.name === tarefa.name;
      const reallyNew = this.tarefas.filter(sameName).length == 0;
      if (reallyNew) {
        this.tarefas.push({
          name: tarefa.name,
          pending: tarefa.pending || true
        });
      }
    },
    tarefaDeletada(i){
      this.tarefas.splice(i, 1)
    },
    statusChange(i){
      this.tarefas[i].pending = !this.tarefas[i].pending
    }
  }
};
</script>

<style>
body {
  font-family: "Lato", sans-serif;
  background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
  color: #fff;
}

#app {
  display: flex;
  flex: 1;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

#app h1 {
  margin-bottom: 5px;
  font-weight: 300;
  font-size: 3rem;
}

</style>
