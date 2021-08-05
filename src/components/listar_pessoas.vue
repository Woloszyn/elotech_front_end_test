<template>
    <div id="listar_pessoas">
        <center>
            <table>
                <thead>
                    <th> Id </th>
                    <th> Nome </th>
                    <th> CPF </th>
                    <th> Data Nascimento </th>
                    <th> Contatos </th>
                    <th></th>
                    <th></th>
                    <th></th>
                    <th>Remover</th>
                    <th>Editar</th>
                </thead>
                <tbody>
                    <tr v-for="pessoa in pessoas" :key='pessoa.id'>
                        <td>{{pessoa.id}}</td>
                        <td>{{pessoa.nome}}</td>
                        <td>{{pessoa.cpf}}</td>
                        <td>{{pessoa.dataNascimento}}</td>
                        <td colspan="4">
                            <ul>
                                <li v-for="contato in pessoa.contato" :key="contato.id">
                                    #{{contato.id}} - {{contato.nome}} - {{contato.email}} - {{contato.telefone}}
                                </li>
                            </ul>
                        </td>
                        <td>
                            <button @click="remover(pessoa.id)"> Remover </button>
                        </td>
                        <td>
                            <button @click="editar(pessoa)"> Editar </button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </center>
        <center>
            <button @click="recuperaPessoas(0, pessoas.length + 10)">Carregar próximos 10</button>
        </center>
    </div>
</template>

<script>
export default {
    data: () => {
        return {
            pessoas: []
        }
    },
    methods: {
        recuperaPessoas(comeco, fim) {
            this.axios.get(`http://apielotech.woloszyn.tech/getPessoas/Paginate/${comeco}/${fim}`).then((result) => {
                console.log(result);
                this.pessoas = result.data;
            })
        },
        remover(pessoa_id) {
            this.axios.delete("http://apielotech.woloszyn.tech/deletePessoa/"+pessoa_id).then(() => {
                this.recuperaPessoas(0, 10);
            })
        },
        editar(pessoa) {
            this.$root.$emit('editar', pessoa);
        }
    },
    mounted() {
        this.recuperaPessoas(0, 10);
    }
}
</script>

<style>

    td > button  {
        width: 100%;
    }

    table {
        border: white solid 1px;
    }

    th {
        border-bottom: white solid 2px;
        font-size: 1.5rem;
    }
    td {
        border-bottom: white solid 1px;
    }
    td > ul > li {
        padding: 5px;
    }

</style>