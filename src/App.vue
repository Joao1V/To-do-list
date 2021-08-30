<template>
  <h1 class="mt-32 text-center text-4xl font-bold text-gray-600">{{ titulo }}</h1>
  <div class="container p-10 text-white bg-blue-400 md:w-1/2 lg:w-1/2 mx-auto mt-10 rounded">
    <app-input>
      <input
        class="outline-none w-full"
        v-model="tarefa.descricao"
        type="text"
        placeholder="Descrição da tarefa"
      />
    </app-input>
    <app-btn class="mt-3 mx-auto" @click="adicionarTarefa">Adicionar</app-btn>
  </div>

  <table class="table-fixed border-collapse border border-blue-600 mx-auto mt-10 w-4/5 md:w-1/2 lg:w-1/2">
    <thead>
      <th class="border border-blue-600 px-5 py-3">Concluída</th>
      <th class="w-1/2 border border-blue-600 px-5 py-3">Descrição</th>
      <th class="border border-blue-600 px-5 py-3">Remover</th>
    </thead>
    <tbody>
      <tr v-for="(iterador,ind) in tarefas" :key="iterador" :class="{ riscado: iterador.concluida }">
        <td class="border border-blue-600 px-5 py-3">
          <input type="checkbox" v-model="iterador.concluida"/>
        </td>
        <td class="border border-blue-600 px-5 py-3 box-border">
          {{ iterador.descricao }}
        </td>
        <td class="border border-blue-600 px-5 py-3 ">
          <app-trash @click="remover(ind)" ></app-trash>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script setup>
import AppBtn from "./components/AppBtn.vue";
import AppTrash from "./components/AppTrash.vue";
import AppInput from "./components/AppInput.vue"
import { reactive, ref } from "vue"

// Composition API
const titulo = ref("Todo list")
const tarefas = reactive([])
const tarefa = reactive({
  descricao: "",
  concluida: false
})

function adicionarTarefa() {
  tarefas.push(Object.assign({}, tarefa));
}

function remover(ind) {
  tarefas.splice(ind,1) // A partir da posição indice quantos elementos quero remover.
}
</script>

<style>
.riscado {
  text-decoration: line-through;
}
</style>