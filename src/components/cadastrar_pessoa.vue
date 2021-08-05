<template>
    <div id='cadastro_pessoa'>
        <center>
            <div class="info_pessoas">
                <label for="name">Nome</label>
                <br>
                <input type="text" v-model="nome" placeholder="John Boe">
                <br>
                <label for="name">Cpf</label>
                <br>
                <input type="text" v-model="cpf" placeholder="XXXXXXXXXX">
                <br>
                <label for="name">Data de nascimento</label>
                <br>
                <input type="text" v-model="dataNascimento" placeholder="01-01-0001">
            </div>
        </center>
        <center>
            <div class="grid_contatos">
                <h2>Contatos</h2>
                <hr>
                <div class="item_contato" v-for="contato in contatos" :key="contato.id">
                    <contato-add :contato="contato"></contato-add>
                </div>
                <button @click="adiciona_contato()">+</button>
                <button @click="remove_contato()">-</button>
            </div>
        </center>
        <div class="acoes">
            <button @click="request_add()">Adicionar</button>
            <button @click="limpa()">Limpar</button>
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
            contatos : [{ 'nome': '', 'email':'', 'telefone':'' }]
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
        limpa() {
            this.id = ''
            this.nome = ''
            this.cpf = ''
            this.dataNascimento = ''
            this.contatos = [{ 'nome': '', 'email':'', 'telefone':'' }];
        },
        request_add() {
            if(this.id == '') {
                let dados = new FormData();
                dados.append('nome', this.nome);
                dados.append('cpf', this.cpf);
                dados.append('dataNascimento', this.dataNascimento);
                dados.append('contatos', btoa(JSON.stringify(this.contatos)));
                this.axios.post('http://apielotech.woloszyn.tech/createPessoa', dados).then((response) => {
                    console.log(response)
                    this.limpa();
                    this.$root.$emit('add_pessoa');
                }).catch((error) => {
                    this.$root.$emit('error', error.response.data)
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
            this.axios.put('http://apielotech.woloszyn.tech/updatePessoa', dados).then((response) => {
                console.log(response)
                this.limpa();
                this.$root.$emit('add_pessoa');
            }).catch((error) => {
                this.$root.$emit('error', error.data)
            })
        }
    },
    mounted() {
        this.$root.$on('editar', (pessoa)  => {
            this.id = pessoa.id
            this.nome = pessoa.nome
            this.cpf = pessoa.cpf
            this.dataNascimento = pessoa.dataNascimento
            this.contatos = pessoa.contato
        })
    }

}
</script>

<style>

    #cadastro_pessoas {
        align-content: center;
        font-size: 15px;
    }

    .grid_contatos{
        border: white solid 1px;
        width: 60%;
        padding: 15px;
        align-content: center;
        border-radius: 5px;
    }
    .item_contato{
        border: white solid 1px;
        width: 90%;
        padding: 15px;
        border-radius: 5px;
        align-content: center;
    }

    .item_contato >input{
        width: 60%;
    }

    .info_pessoas{
        width: 40%;
        margin: 15px;
        border: white solid 1px;
        padding: 15px;
    }

    .info_pessoas >input{
        width: 100%;
    }

    button {
        width: 20%;
        height: 2rem;
        background-color: white;
        color: green;
        border: transparent solid 1px;
        border-radius: 5px;
    }

</style>