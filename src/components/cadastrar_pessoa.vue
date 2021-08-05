<template>
    <div id='cadastro_pessoa'>
        <label for="name">Nome</label>
        <input type="text" v-model="nome" placeholder="nome">
        <br>
        <label for="name">Cpf</label>
        <input type="text" v-model="cpf" placeholder="somente números">
        <br>
        <label for="name">Data de nascimento</label>
        <input type="text" v-model="dataNascimento" placeholder="01-01-0001">
        <div class="grid_contatos">
            <div class="item_contato" v-for="contato in contatos" :key="contato.id">
                <contato-add :contato="contato"></contato-add>
            </div>
            <button @click="adiciona_contato()">+</button>
            <button @click="remove_contato()">-</button>
        </div>
        <div class="acoes">
            <button @click="request_add()">Adicionar</button>
            <button>Limpar</button>
        </div>
    </div>
</template>

<script>

import contato_add from './contato_add.vue'

export default {

    components: {
        'contato-add': contato_add
    },
    data: () => {
        return {
            id : '',
            nome : '',
            cpf: '',
            dataNascimento: '',
            contatos : [{ 'nome': 'Eduardo', 'email':'example@example.com', 'telefone':'54999937992' }]
        }
    },
    methods: {
        adiciona_contato()  {
            this.contatos.push({
                'nome': '',
                'email': '',
                'telefone': ''
            })
        },
        remove_contato()  {
            if(this.contatos.length > 1) {
                this.contatos.pop();
            }
        },
        recebeDadosAlteracao(dados) {
            this.id = dados.id
            this.nome = dados.nome
            this.dataNascimento = dados.dataNascimento
            this.contatos = dados.contato
        },
        request_add() {
            if(this.id == '') {
                let dados = new FormData();
                dados.append('nome', this.nome);
                dados.append('cpf', this.cpf);
                dados.append('dataNascimento', this.dataNascimento);
                dados.append('contatos', btoa(JSON.stringify(this.contatos)));
                this.axios.post('http://localhost:8078/createPessoa', dados).then((response) => {
                    console.log(response)
                }).catch((error) => {
                    console.log(error)
                })
            } else {
                this.request_update();
            }
        },
        request_update() {
            let dados = new FormData();
            dados.append('id', this.id);
            dados.append('nome', this.nome);
            dados.append('cpf', this.cpf);
            dados.append('dataNascimento', this.dataNascimento);
            dados.append('contatos', btoa(JSON.stringify(this.contatos)));
            this.axios.put('http://localhost:8078/updatePessoa', dados).then((response) => {
                console.log(response)
            }).catch((error) => {
                console.log(error)
            })
        }
    }

}
</script>

<style>

</style>