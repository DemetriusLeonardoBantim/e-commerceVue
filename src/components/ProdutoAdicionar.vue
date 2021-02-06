<template>
  <form class="adicionar-produto">
    <label for="nome">Nome</label>
    <input type="text" name="nome" id="nome" v-model="produto.nome">
    <label for="preco">Preco (R$) </label>
    <input type="text" name="preco" id="preco" v-model="produto.preco">
    <label for="fotos">Foto </label>
    <input type="file" name="fotos" id="fotos" ref="fotos" >
    <label for="descricao">Descricao</label>
    <textarea name="descricao" id="descricao" v-model="produto.descricao"></textarea>
    <input  class="btn" type="button" value="Adicionar Produto" @click.prevent="adicionarProduto">
  </form>
</template>

<script>
import {api} from '../services'
export default {

  name:"ProdutoAdicionar",
  data(){
    return {
      produto: {
        nome:'',
        preco: '',
        descricao:'',
        fotos: null,
        vendido: "false"
      }
    }
  },
  methods:{
    formatarProduto(){
      this.produto.usuario_id = this.$store.state.usuario_id
    },
    adicionarProduto() {
      this.formatarProduto()
      api.post("/produto", this.produto).then(() =>{
        this.$store.dispatch('getUsuarioProdutos')
      })
    }
  }
}
</script>

<style scoped>
.adicionar-produto{
  display: grid;
  grid-template-columns: 100px 1fr;
  align-items: center;
  margin-bottom: 60px;
}

.btn{
  grid-column: 2;

}
</style>
