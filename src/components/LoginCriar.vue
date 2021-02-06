<template>
  <section>
    <h2>Crie a sua conta</h2>
    <transition mode="out-in">
      <button  v-if="!criar" @click="criar = true" class="btn criar" >Criar conta</button>
      <UsuarioForm v-else>
        <button class="btn" @click.prevent="criarUsuario">Criar usuario</button>
      </UsuarioForm>
    </transition>

  </section>
</template>

<script>
import UsuarioForm from './UsuarioForm.vue'

export default {
  name: 'LoginCriar',
  components:{
    UsuarioForm
  },
  data(){
    return{
      criar: false
    }
  },
  methods:{
     async criarUsuario(){
      try{
        await this.$store.dispatch("criarUsuario", this.$store.state.usuario)
        await this.$store.dispatch("getUsuario", this.$store.usuario.email)
        this.$router.push({name: "usuario"})
     }catch(error){
       console.log(error)
     }
   }
  }
}
</script>

<style scoped>
h2{
  text-align: center;
  margin-top: 40px;
  margin-bottom: 10px;
}

.btn{
  width: 100%;
  max-height: 300px;
  margin-left: auto;
  margin-right: auto;
}


</style>
