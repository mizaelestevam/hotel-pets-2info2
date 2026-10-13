<script setup>
import { onMounted, ref } from 'vue';
import { useRoute } from 'vue-router';

const route = useRoute(); // chamando meu router
const API_URL = 'http://localhost:3000';

const tutor = ref(null);

async function carregarTutor() {
// pegando o id do tutor que esta na url do negavor;
const idTutor = route.params.id;

// chamando a API para buscar pet pelo id;
const respostaTutor = await fetch(`${API_URL}/tutores/${idTutor}`);
console.log('respostaTutor', respostaTutor);

//convertendo a resposta da API para JSON;
tutor.value = await respostaTutor.json();
console.log('tutor', tutor.value);

}

onMounted(carregarTutor)

</script>

<template>
<section v-if="tutor === null">
<p>Carregando...</p>
</section>

<section v-else>


<h1>Nome do Tutor: {{tutor.nome}}</h1>
<p>Telefone: {{ tutor.telefone }}</p>

</section>

</template>