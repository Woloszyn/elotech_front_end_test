<template>
  <div id="app">
      <nav>
        <button @click="menu = 1">Criar Pessoa</button> |
        <button @click="menu = 2">Listar pessoas</button>
      </nav>
      <cadastropessoa ref="cadastropessoa" v-show="menu == 1"></cadastropessoa>
      <listarpessoas ref="listaPessoas" v-show="menu == 2"></listarpessoas>
      <span v-show="showError">
        {{msg_erro}}
      </span>
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
        menu: 1,
        pessoaParam: {},
        showError: false,
        msg_erro: ''
    }
  },
  mounted() {
    this.$root.$on('editar', (pessoa) => {
        this.menu = 1;
        let p = pessoa;
        console.log(p)
    });
    this.$root.$on('error', (mensagem_erro) => {
        this.showError = true;
        this.msg_erro = mensagem_erro
    });
    this.$root.$on('add_pessoa', () => {
      this.$refs.listaPessoas.recuperaPessoas(0,10);
    })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  margin-top: 60px;
}
body{
  background-image: url("https://i.ytimg.com/vi/XBPjVzSoepo/maxresdefault.jpg");
  background-repeat: no-repeat;
  background-size: cover;
}
</style>
