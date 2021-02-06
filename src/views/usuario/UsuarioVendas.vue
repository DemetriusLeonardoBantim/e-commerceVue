<template>
  <section>
    <div v-if="compras">
      <h2>Compras</h2>
      <div class="produtos-wrapper" v-for="(compra,index) in compras" :key="index">
        <ProdutoItem v-if="compra.produto" :produto="compra.produto">
          <p class="vendedor"><span>Vemdedor</span>{{compra.vendedos_id}}</p>
        </ProdutoItem>
        <div class="entrega">
          <h3>Entrega:</h3>
          <ul v-if="venda.endereco">
            <li v-for="(value,key) in venda.endereco" :key="key">
              {{key}}
              {{value}}
            </li>
          </ul>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import ProdutoItem from '../../components/ProdutoItem'
import {api} from '../../services'
import {mapState} from 'vuex'


export default {
  components:{
    ProdutoItem
  },
data(){
    return{
      vendas: null,
    }
  },
  computed:{
    ...mapState(["usuario"])
  },
  methods : {
    getVendas(){
      api.get(`/transacao?vendedor_id=${this.usuario.id}`).then(response => {
        this.vendas = response.data;
      })
    }
  },
  watch:{
    login(){
      this.getVendas()
    }
  },
  created() {
    if(this.login){
     this.getVendas()
    }
  }
}
</script>

<style scoped>

.produto-wrapper{
  margin-bottom: 40px
}

.vendedor span{
  color: #e80;
}

h2{
  margin-bottom: 20px;
}
.entrega{
  display: grid;
  grid-template-columns: minmax(100px, 200px) 1fr;
  grid-gap: 20px;
  margin-bottom: 60px;
}
h2{
  margin-bottom: 20px;
}

h3{
  margin:0px ;
  justify-self: end;
}
</style>
