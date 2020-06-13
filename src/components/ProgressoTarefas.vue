<template>
  <div class="tarefas-progresso">
    <span class="progresso-value">{{ progress }}%</span>
    <div class="barra-progresso" :style="{width: progress + '%'}"></div>
  </div>
</template>
<script>
export default {
  props: {
    progress: { type: Number, default: 0 }
  }
};
</script>
<style scoped>
.tarefas-progresso {
  position: relative;
  border: 1px solid darkorchid;
  color: #ffff;
  border-radius: 8px;
  width: 50%;
  margin-top: 5px;
  margin-bottom: 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.barra-progresso {
  position: absolute;
  height: 100%;
  border-radius: 8px;
  background-color: rebeccapurple;
  align-self: flex-start;
}

.progresso-value {
  color: #ffff;
  z-index: 1;
  font-size: 1.2rem;
}
</style>