<script setup>
import { ref } from 'vue'
const tarefas = ref([
  {
    id: 1,
    tarefa: 'Tarefa 1',
    status: 'concluida'
  },
  {
    id: 2,
    tarefa: 'Tarefa 2',
    status: 'concluida',
  },
  {
    id: 3,
    tarefa: 'Tarefa 3',
    status: 'pendente'
  },
  {
    id: 4,
    tarefa: 'Tarefa 4',
    status: 'pendente'
  }
])
const novaTarefa = ref('')

function removerTarefa(item) {
  let index = tarefas.value.findIndex((e) => e == item)
  tarefas.value.splice(index, 1);
}

function adicionarTarefa() {
  tarefas.value.push()
}

</script>

<template>
  <div class="container">
    <h1>Lista de Tarefas</h1>
    <ul>
      <li v-for="item in tarefas" :key="item.id">
        {{ item.tarefa }}
      </li>
    </ul>
    <input type="text" v-model="novaTarefa">
    <button @click="tarefas.push(novaTarefa)">Adicionar</button>
  </div>
</template>

<style scoped></style>