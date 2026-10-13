<script setup>
import { onMounted, ref } from 'vue';
import { RouterLink } from 'vue-router';


const tutores = ref([]); // lista de tutores vazia;

// chamando a minha API geral:
const API_URL = 'http://localhost:3000';

// chamar a minha API para listar todos os pets e tutores;
async function carregarDados() {
 

  const respostaTutores = await fetch(`${API_URL}/tutores`);
  tutores.value = await respostaTutores.json();

 
  console.table(tutores.value);
}


  
async function excluirTutor(id) {
const confirmarExclusao = window.confirm('Deseja realmente excluir este tutor?');

if (confirmarExclusao) {
  await fetch(`${API_URL}/tutores${id}`, {
    method: 'DELETE',
  });
  await carregarDados(); // Recarregar os dados após a exclusão
}
}

onMounted(carregarDados);
</script>

<template>
  <div>
    <header class="mb-4">
      <h1 class="text-2xl font-bold">Listagem de Tutores</h1>
      <p class="text-body-secondary mb-0">
        Listagem dos Tutores cadastrados.
      </p>
    </header>

    <RouterLink
      class="btn btn-outline-primary"
      to="tutores/novo"
    >
      Novo tutor
    </RouterLink>

<table class="table table-striped table-hover">
      <thead>
        <tr>
          <th>ID</th>
          <th>Nome</th>
          <th>Telefone</th>
          <th>Ações</th>
          
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="tutor in tutores"
          :key="tutor.id"
        >
          <td>{{ tutor.id }}</td>
          <td>{{ tutor.nome }}</td>
          <td>{{ tutor.telefone }}</td>
          <td>
            <RouterLink :to="`/tutores/${tutor.id}`">Visualizar</RouterLink>
            <button class="btn btn-danger" @click="excluirTutor(tutor.id)">Excluir</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>

</template>


