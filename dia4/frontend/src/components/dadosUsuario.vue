<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="info">
      <b-navbar-brand>Dados do usuário</b-navbar-brand>
      <b-navbar-nav class="ml-auto">
        <b-button v-on:click="$bvModal.show('modal-insert')">
          <b-icon-plus></b-icon-plus>
        </b-button>
      </b-navbar-nav>
    </b-navbar>
    <b-alert v-model="mostrarErro" variant="danger" dismissible>
      Falha ao {{errorMessage.action}} - {{errorMessage.message}}
    </b-alert>
    <FormProduto ref="formAdicionar" :produto="newProduto" title="Adicionar Dado" v-on:confirmed="adicionarDado" idModal="modal-insert"/>
    <ul id="dados_usuario">
        <li v-for="dados_usuario, index in dados_usuario" v-bind:key="dados_usuario.codigo">
            <Produto v-bind:dados_usuario="dados_usuario" :index="index" v-on:removed="removerDado(index, dados_usuario)" v-on:edited="editarDado"/>
        </li>
    </ul>
  </div>
</template>
<script>
import Produto from './Produto.vue'
import FormProduto from './FormProduto.vue'
import axios from 'axios'
export default {
    name: 'ListaProdutos',
    data: function() {
        return {
            produtos: [],
            newProduto: {
              codigo: '',
              descricao: '',
              quantidade: ''
            },
            mostrarErro: false,
            errorMessage: {
              action: '',
              message: ''
            }
        }
    },
    components: {
        Produto,
        FormProduto
    },
    methods: {
      removerProduto: async function(index, produto) {
        // envie o comando de excluir para o backend
        await axios.delete(`http://localhost:3000/produtos/${produto.codigo}`)
        this.produtos.splice(index, 1)
      },
      adicionarProduto: async function(produto) {
        try {
          console.log("Adcionair prdouto")
          console.log(produto)
          var result = await axios.post("http://localhost:3000/produtos", produto)
          this.produtos.push(result.data)
        } catch (error) {
          this.mostrarErro = true;
          this.errorMessage.action = "inserir"
          this.errorMessage.message = error.response.statusText
        }
        this.$refs.formAdicionar.reset();
      },
      editarProduto: async function(produto, index) {
        try {
          var result = await axios.put(`http://localhost:3000/produtos/${this.produtos[index].codigo}`, produto)
          this.produtos[index].codigo = result.data.codigo
          this.produtos[index].descricao = result.data.descricao
          this.produtos[index].quantidade = result.data.quantidade
        } catch (error) {
          this.mostrarErro = true;
          this.errorMessage.action = "atualizar"
          this.errorMessage.message = error.response.statusText
        }
      }
    },
    async created() {
      var response = await axios.get('http://localhost:3000/produtos')
      this.produtos = response.data
    }
}
</script>
<style scoped>
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin: 0 10px;
}
</style>