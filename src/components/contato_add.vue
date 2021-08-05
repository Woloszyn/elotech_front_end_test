<template>
    <div class="contato_add">
        <label for="nome_contato">Nome</label>
        <input type="text" placeholder="Contato" v-model="contato.nome" >
        <br>
        <label for="nome_contato">Email</label>
        <input type="text" placeholder="example@example.com" v-model="contato.email" >
        <br>
        <label for="nome_contato">Telefone</label>
        <input type="text" v-model="contato.telefone" placeholder="(##)########" >
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

</style>