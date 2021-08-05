<template>
    <div id="listar_pessoas">
        <ul>
            <li v-for="pessoa in pessoas" :key='pessoa.id'>
                #{{pessoa.id}} - {{pessoa.nome}}
                <span>Contatos </span>
                <br>
                <div v-for="contato in pessoa.contato" :key="contato.id">
                        #{{contato.id}} - {{contato.nome}} - {{contato.email}} - {{contato.telefone}}
                </div>
                <button @click="remover(pessoa.id)"> Remover </button>
                <button> Editar </button>
            </li>
        </ul>
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
        recuperaPessoas() {
            this.axios.get("http://localhost:8078/getPessoas").then((result) => {
                console.log(result);
                this.pessoas = result.data;
            })
        },
        remover(pessoa_id) {
            this.axios.delete("http://localhost:8078/deletePessoa/"+pessoa_id).then(() => {
                this.recuperaPessoas();
            })
        }
    },
    mounted() {
        this.recuperaPessoas();
    }
}
</script>

<style>

</style>