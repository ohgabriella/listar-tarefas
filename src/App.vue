<template>
  <div id="app">
    <h1>Tarefas</h1>
    <ProgressoTarefas :progress="progress" />
    <NovaTarefa @tarefaAdicionada="addTarefa"></NovaTarefa>
    <GridTarefas @deletarTarefa="tarefaDeletada" @changeStatus="statusChange" :tarefas="tarefas" />
  </div>
</template>

<script>
import NovaTarefa from "./components/NovaTarefa";
import GridTarefas from "./components/GridTarefas";
import ProgressoTarefas from "./components/ProgressoTarefas";

export default {
  components: { NovaTarefa, GridTarefas, ProgressoTarefas },
  data() {
    return {
      tarefas: []
    };
  },
  computed: {
    progress() {
      const total = this.tarefas.length;
      const done = this.tarefas.filter(t => !t.pending).length;
      return Math.round((done / total) * 100) || 0;
    }
  },
  watch: {
    tarefas: {
      deep: true,
      handler() {
        localStorage.setItem("tarefas", JSON.stringify(this.tarefas));
      }
    }
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
    tarefaDeletada(i) {
      this.tarefas.splice(i, 1);
    },
    statusChange(i) {
      this.tarefas[i].pending = !this.tarefas[i].pending;
    }
  },
  created() {
    const json = localStorage.getItem("tarefas");
    const array = JSON.parse(json);
    if (Array.isArray(array)) {
      this.tarefas = array;
    } else {
      this.tarefas = [];
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
