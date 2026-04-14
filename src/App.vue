<script setup>
import { ref, computed } from 'vue'

import tarefaChild from './components/TarefaChild.vue'
import buttonChild from './components/ButtonChild.vue'

const tarefas = ref([
  {
    id: 1,
    tarefa: 'Tarefa 1',
    status: 'concluida',
  },
  {
    id: 2,
    tarefa: 'Tarefa 2',
    status: 'concluida',
  },
  {
    id: 3,
    tarefa: 'Tarefa 3',
    status: 'pendente',
  },
  {
    id: 4,
    tarefa: 'Tarefa 4',
    status: 'pendente',
  },
])
const filtro = ref('')


function addTarefa(novaTarefa) {

  let id = 1
  if (tarefas.value.length > 0) {
    id = tarefas.value[tarefas.value.length - 1].id + 1
  }
  tarefas.value.push({ id: id, tarefa: novaTarefa, status: 'pendente' })
}

function editTarefa(id) {
  const novoNome = prompt('Insira o novo nome da tarefa:')
  if (novoNome.trim() != '') {
    tarefas.value[id - 1].tarefa = novoNome
  }

}

const tarefasFiltradas = computed(() => {
  if (filtro.value.trim().length > 0) {
    return tarefas.value.filter((item) => item.tarefa.includes(filtro.value))
  } else {
    return tarefas.value
  }
})
const novaTarefa = ref('')

function removerTarefa(item) {
  let index = tarefas.value.findIndex((e) => e == item)
  tarefas.value.splice(index, 1)
}


const concluidas = computed(() => {
  return tarefas.value.filter(t => t.status === 'concluida').length
})

const pendentes = computed(() => {
  return tarefas.value.filter(t => t.status === 'pendente').length
})
</script>

<template>
  <div class="container">
    <h1>Lista de Tarefas</h1>
    <input type="text" v-model="novaTarefa" />
    <buttonChild @click="addTarefa(novaTarefa)" :basic="'btn'">Adicionar</buttonChild>
    <ul>
      <tarefaChild v-for="item in tarefasFiltradas" :key="item"
        @click="item.status = item.status === 'concluida' ? 'pendente' : 'concluida'" :status="item.status"
        :nome="item.tarefa">
        {{ item.tarefa }} <buttonChild @click="editTarefa(item.id)" :basic="'btn'">Edit</buttonChild>
        <buttonChild @click="removerTarefa(item)" :basic="'btn'">Delete</buttonChild>
      </tarefaChild>
      <p v-if="tarefasFiltradas.length === 0">Nenhuma Tarefa Encontrada!</p>
    </ul>

    <input type="search" v-model="filtro" placeholder="filtrar tarefas">
    <p>Concluídas: {{ concluidas }}</p>
    <p>Pendentes: {{ pendentes }}</p>
  </div>
</template>

<style scoped></style>
