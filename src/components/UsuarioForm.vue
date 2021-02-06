<template>
  <form action="">
    <div v-if="mostrarDadosLogin">
      <label for="nome">Nome</label>
      <input type="text" name="nome" id="nome" v-model="nome">
      <label for="emailForm">Email</label>
      <input type="text" name="emailForm" id="emailForm" v-model="email">
      <label for="senhaForm">Senha</label>
      <input type="password" name="senhaForm" id="senhaForm" v-model="senha">
    </div>

    <label for="cep">Cep</label>
    <input type="text" name="cep" id="cep" v-model="cep" @keyup="preencherCep">
    <label for="rua">Rua</label>
    <input type="text" name="rua" id="rua" v-model="rua">
    <label for="numero">Numero</label>
    <input type="text" name="numero" id="numero" v-model="numero">
    <label for="bairro">Bairro</label>
    <input type="text" name="bairro" id="bairro" v-model="bairro">
    <label for="cidade">Cidade</label>
    <input type="text" name="cidade" id="cidade" v-model="cidade">
    <label for="estado">Estado</label>
    <input type="text" name="estado" id="estado" v-model="estado">

  <div class="button">
    <slot></slot>
  </div>
  </form>
</template>

<script>
import {mapFields} from '../helpers.js'
import {getCep} from '../services'

export default {
  computed:{
    ...mapFields({
      fields: ["nome", "email", "senha","rua", "cep", "numero","bairro", "cidade", "estado"],
      base: "usuario",
      mutation: "UPDATE_USUARIO"
    }),
    mostrarDadosLogin(){
      return (!this.$store.state.login || (this.$route.name === 'usuario-editar'))
    }
  },
  methods: {
    preencherCep() {
      const cep = this.cep.replace(/\D/g, "")
      if(cep.lenght=== 8){
          getCep(cep).then(response => {
            console.log(response)
            this.rua = response.data.logradouro;
            this.bairro = response.data.bairro;
            this.estado = response.data.uf;
            this.cidade = response.data.localidade;
            console.log('oi')
          })
      }
    }
  }
}
</script>

<style scoped>
  form,.usuario{
    display: grid;
    grid-auto-columns: 1fr 80px;
    align-items: center;
}

.usuario{
  grid-column: 1/3;
}

.button{
  grid-column: 2;
  margin-top: 10px;
}

</style>
