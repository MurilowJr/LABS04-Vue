<template>
  <div class="about">
    <h1>Bem vindo {{ nome }}</h1>
  <input type="text" v-model="nome" />
  <p v-if="nome.length > 5">Nome grande</p>
  <p v-else>Nome pequeno</p>
  <table>
    <thead>
      <td>Id</td>
      <td>Nome</td>
    </thead>
    <tr v-for="usuario in usuarios" :key="usuario.id">
      <td>{{ usuario.id }}</td>
      <td>{{ usuario.nome }}</td>
    </tr>
  </table>
  </div>
</template>

<script setup lang="ts">
import {onMounted, ref} from 'vue';

const nome = ref("nome");
const usuarios = ref();

async function atualizar() {
  usuarios.value = (await axios.get("https://8080-murilowjr-labs04-k9bxrv3gqhe.ws-us105.gitpod.io")).data;  
}

onMounted(() => {
  atualizar();
});
</script>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
