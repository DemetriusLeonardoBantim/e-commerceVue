<template>
  <section>
  <h2>Endereco para enviar a compra</h2>
  <UsuarioForm>
    <button class="btn" @click.prevent="FinalizarCompra">Finalizar compra</button>
  </UsuarioForm>

  </section>

</template>

<script>
import UsuarioForm from './UsuarioForm'
import {api} from '../services.js'
import {mapState} from 'vuex'


export default {
  name: "FinalizarCompra",
  components: {
    UsuarioForm
  },
  props: ['produto'],
  computedd:{
    ...mapState(['usuario']),
    compra(){
      return {
        comprador_id: this.usuario.email,
        vendedos_id: this.produto.usuario_id,
        produto: this.produto,
        endereco: {
          cep: this.usuario.cep,
          rua: this.usuario.rua,
          numero: this.usuario.numero,
          bairro: this.usuario.bairro,
          cidade: this.usuario.cidade,
          estado: this.usuario.estado
        }
      }
    }
  },
  methods:{
    criarTransacao(){
     return api.post("/transacao", this.compra).then(() => {
        this.$router.push({name : "compras"})
      });
    },
    async criarUsuario(){
      try{
        await this.$store.dispatch("criarUsuario", this.$store.state.usuario)
        await this.$store.dispatch("getUsuario", this.$store.state.usuario.email);
        await this.criarTransacao()
      } catch(error){
        console.log(error)
      }

    },
    finalizarCompra(){
      if(this.$store.state.login){
      this.criarTransacao()
      } else{
        this.criarUsuario()
      }

    }
  }
}
</script>

<style>

</style>
