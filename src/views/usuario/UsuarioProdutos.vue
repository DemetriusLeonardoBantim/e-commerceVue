<template>
  <section>
    <h2>Adicionar Produto</h2>
    <ProdutoAdicionar/>
      <transition-group v-if="usuario_produtos" nome="list" tag="ul">
        <li v-for="(produto,index) in usuario_produtos" :key="index">
          <ProdutoItem :produto="produto">
            <p>{{produto.descricao}}</p>
            <button class="deletar" @click="deletarProduto(produto.id)">Deletar</button>
          </ProdutoItem>
        </li>
      </transition-group>

    <h2>Seus produtos</h2>
  </section>
</template>

<script>
import ProdutoAdicionar from '../../components/ProdutoAdicionar'
import {mapState, mapActions} from 'vuex'
import ProdutoItem from '../../components/ProdutoItem.vue'
import {api} from '../../services'

export default {
  name:"UsuarioProdutos",
  components: {
    ProdutoAdicionar,
    ProdutoItem,
    },
    computed: {
      ...mapState(["login", "usuario", "usuario_produtos"])
    },
    methods: {
      ...mapActions(["getUsuarioProdutos"]),
      deletar(id){
        const confirmar = window.confirm("Deseja remover este produto?")
        if(confirmar){
          api.delete(`/produto/${id}`).then(() =>{
            this.getUsuarioProdutos()
          }).catch(error => {
            console.log(error.response)
          })
        }
      }
    },
    watch: {
      login(){
        this.getUsuarioProdutos()
      }
    },
    created(){
      if(this.login){
        this.getUsuarioProdutos()
      }
    }
}
</script>
<style scoped>
h2{
  margin-bottom: 20px;
}

.list-enter-active,.list-leave-active{
  transition: all .3s;
}

</style>
