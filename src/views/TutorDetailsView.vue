<script setup>
import { onMounted, ref } from 'vue';
import { useRoute } from 'vue-router';

const route = useRoute(); // chamando meu router
const API_URL = 'http://localhost:3000';

const tutor = ref(null);

async function carregarPet() {
// pegando o id do tutor que esta na url do negavor;
const idTutor = route.params.id;

// chamando a API para buscar pet pelo id;
const respostaPet = await fetch(`${API_URL}/pets/${idPet}`);
console.log('respostaPet', respostaPet);

//convertendo a resposta da API para JSON;
console.log('tutor.value', tutor.value);

// chamando a API para buscar o tutor pelo id;
const respostaTutor = await fetch(`${API_URL}/tutores/${tutor.value.Id}`);
tutor.value = await respostaTutor.json();
console.log('Tutor, tudo.value', tutor.value);
}

onMounted(carregarPet)

</script>

<template>
<section v-if="pet === null">
<p>Carregando...</p>
</section>

<section v-else>


<h1>Nome do Tutor: {{tutor.nome}}</h1>
<p>Telefone: {{ tutor.telefone }}</p>

</section>

</template>