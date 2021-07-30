<template>
    <b-modal :id="idModal ? idModal : ('modal-confirm-edit-'+dados_usuario.codigo)" :title="title" v-on:ok="ok()" v-on:cancel="reset()">
        <b-form>
            <b-form-group
            id="input-codigo"
            label="Código"
            label-for="codigo"
            description="Código do usuário"
            ></b-form-group>
            <b-form-input 
            v-model="produtoInterno.codigo"
            type="number"
            required
            ></b-form-input>
            <b-form-group
            id="input-nome"
            label="Nome"
            label-for="nome"
            description="nome do usuário"
            ></b-form-group>
            <b-form-input 
            id="nome"
            v-model="produtoInterno.nome"
            type="text"
            required
            ></b-form-input>
            <b-form-group
            id="input-login"
            label="Login"
            label-for="login"
            description="Login do usuário"
            ></b-form-group>
            <b-form-input 
            id="login"
            v-model="produtoInterno.login"
            type="text"
            required
            ></b-form-input>
            <b-form-group
            id="input-email"
            label="Email"
            label-for="email"
            description="Email do usuário"
            ></b-form-group>
            <b-form-input 
            id="email"
            v-model="produtoInterno.email"
            type="text"
            required
            ></b-form-input>
        </b-form>
    </b-modal>
</template>

<script>
export default {
    name: "FormProduto",
    data: function() {
        return {
            produtoInterno: {
                codigo: '',
                descricao: '',
                quantidade: ''
            }
        }
    },
    props: {
        title: String,
        idModal: String,
        produto: {
            codigo: Number,
            descricao: String,
            quantidade: Number
        }
    },
    methods: {
        ok: function() {
            this.$emit('confirmed', this.produtoInterno)
        },
        reset: function() {
            this.produtoInterno.codigo = this.produto.codigo
            this.produtoInterno.descricao = this.produto.descricao
            this.produtoInterno.quantidade = this.produto.quantidade            
        }
    },
    mounted() {
        this.reset();
    }
}
</script>

<style>
</style>