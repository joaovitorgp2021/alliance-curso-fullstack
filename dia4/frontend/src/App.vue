<template>
  <div id="app">
    <dados.usuario/>
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import dados_usuario from './components/dados_usuario.vue'
export default {
  name: 'App',
  components: {
    dados_usuario
  }
}
</script>

<style lang="scss">
@import "~@/assets/scss/vendors/bootstrap-vue/index";
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>