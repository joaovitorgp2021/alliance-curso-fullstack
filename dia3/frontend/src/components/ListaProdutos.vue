<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="info">
      <b-navbar-brand>Produtos</b-navbar-brand>
      <b-navbar-nav class="ml-auto">
        <b-button>
          <b-icon-plus></b-icon-plus>
        </b-button>
      </b-navbar-nav>
      <b-modal :id="'test-'+ produto.codigo" title="insert" 
      ok-variant='danger' cancel-variant="success">
      
  <p> Tem certeza que deseja excluir </p>
      
    </b-navbar>
    <ul id="listaProdutos">
        <li v-for="produto, index in produtos" v-bind:key="produto.codigo">
            <Produto v-bind:produto="produto" v-on:removed="removerProduto(index)"/>
        </li>
    </ul>
  </div>
</template>

<script>