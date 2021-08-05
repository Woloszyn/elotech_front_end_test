<template>
  <div id="app">
      <nav>
        <button @click="menu = 1">Criar Pessoa</button>
        <button @click="menu = 2">Listar pessoas</button>
      </nav>
      <cadastropessoa v-if="menu == 1"></cadastropessoa>
      <listarpessoas v-if="menu == 2"></listarpessoas>
  </div>
</template>

<script>

import cadastropessoa from './components/cadastrar_pessoa.vue';
import listarpessoas from './components/listar_pessoas.vue';

export default {
  name: 'App',
  components: {
    cadastropessoa,
    listarpessoas
  },
  data: () => {
    return {
        menu: 1
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
