<template>
    <div class="contato_add">
        <div class="nome_contato">
            <label for="nome_contato">Nome</label>
            <br>
            <input type="text" placeholder="Contato" v-model="contato.nome" >
        </div>
        <div class="email">
            <label for="nome_contato">Email</label>
            <br>
            <input type="text" placeholder="example@example.com" v-model="contato.email" >
        </div>
        <div class="telefone">
            <label for="nome_contato">Telefone</label>
            <br>
            <input type="text" v-model="contato.telefone" placeholder="(##)########" >
        </div>
    </div>
</template>

<script>
export default {

    props: {
        contato: { required: true, type:Object }
    }

}
</script>

<style>

    input {
        width: 90%;
        border: transparent solid 1px;
        margin-top: 5px;
        border-radius: 5px;
    }

    div{
        margin-bottom: 15px;
    }

</style>