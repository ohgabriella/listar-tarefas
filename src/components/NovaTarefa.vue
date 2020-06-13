<template>
    <div class="nova-tarefa">
        <input v-model="name" 
        @keydown.enter="add" 
        type='text' 
        class="add-tarefa" 
        placeholder="Nova tarefa"
        >
        <button class="add-tarefa">+</button>
    </div>
</template>
<script>
export default {
    data() {
        return {
            name: ''
        }
    },
    methods: {
        add() {
            this.$emit('tarefaAdicionada', {name: this.name})
            this.name = ''
        }
    }
}
</script>
<style scoped>
.nova-tarefa{
    display: flex;
    margin: 30px;
}

.add-tarefa {
    outline: none;
    font: 2rem;
    padding: 5px 10px 8px;
    border: 1px solid #fff;
    color: #fff;
}

input.add-tarefa{
    height: 30px;
    width: 600px;
    border-top-left-radius: 7px;
    border-bottom-left-radius: 7px;
    background-color: #fff2;
}

button.add-tarefa{
    border-left: none;
    border-top-right-radius: 7px;
    border-bottom-right-radius: 7px;
    background-color: rgba(9, 100, 175, 0.133);
}

</style>