<script setup>
import { ref, computed } from 'vue'
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

function addTarefa(novaTarefa){
  const id = tarefas.value [tarefas.value.length - 1].id + 1
  console.log(id)
  tarefas.value.push({id: id, tarefa: novaTarefa, status: 'pendente'})
}

function editTarefa(id){
  const novoNome = prompt("Insira o novo nome da tarefa:");
  tarefas.value[id-1].tarefa = novoNome
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
</script>

<template>
  <div class="container">
    <h1>Lista de Tarefas</h1>
    <ul>
      <li v-for="item in tarefas" :key="item.id">
        {{ item.tarefa }} <button @click="editTarefa(item.id)">Edit</button>
        <button @click="removerTarefa(item)">Delete</button>
      </li>
    </ul>
    <input type="text" v-model="novaTarefa" />
    <button @click="addTarefa(novaTarefa)">Adicionar</button>
    <p>Concluídas: {{  }}</p>
    <p>Pendentes: {{  }}</p>
  </div>
</template>

<style scoped></style>
