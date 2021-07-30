<template>
  <div>
    <b-card id="card-movimentos" class="text-center"
      :title="movimentos.descricao"
      :sub-title="produto.codigo.toString()"
      >
      <b-card-text class="bg-secondary text-light">Quantidade {{produto.quantidade}}</b-card-text>

      <b-button class="float-right" v-b-modal="'modal-confirm-delete-'+produto.codigo">
        <b-icon-trash></b-icon-trash>
      </b-button>

      <b-button class="float-right" v-b-modal="'modal-confirm-edit-'+produto.codigo">
        <b-icon-pen></b-icon-pen>
      </b-button>
    </b-card>
    <b-modal :id="'modal-confirm-delete-'+produto.codigo" title="Confirmação" 
      ok-variant='danger' cancel-variant="success"
      ok-title='Sim' cancel-title='Não'
      v-on:ok="excluir()"
      >
      <p>Tem certeza que deseja excluir o produto</p>
    </b-modal>
    <FormProduto :produto="produto" title="Editar produto" v-on:confirmed="edit"/>
  </div>
</template>

<script>
import FormMovimentos from "./FormMovimentos.vue"
export default {
  name: "Movimentos",
  props: {
    movimentos: {
      id: Number,
      codigo: Number,
      descricao: String,
      quantidade: Number
    },
    index: Number
  },
  methods: {
    excluir: function () {
      // avisar que eu fui excluido
      this.$emit('removed');
    },
    edit: function(movimentos) {
      this.$emit('edited', movimentos, this.index)
    }
  },
  components: {
    FormMovimentos
  }
}
</script>
<style scoped>
.card {
    margin-bottom: 10px;
    max-width: 320px;
}
.card-title {
  text-align: left;
}
.card-subtitle {
  text-align: left;
}
.btn {
  margin: 3px;
}
</style>