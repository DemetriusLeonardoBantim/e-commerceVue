<template>
  <section class="usuario">
    <nav class="sidenav">
      <ul>
        <li>
          <router-link :to="{name: 'usuario'}">Produtos</router-link>
        </li>
        <li>
          <router-link :to="{name: 'compras'}">Compras</router-link>
        </li>
        <li>
          <router-link :to="{name: 'vendas'}">Vendas</router-link>
        </li>
        <li>
          <router-link :to="{name:'usuario-editar'}">Editar usuario</router-link>
        </li>
        <li>
          <button @click.prevent = "deslogar">Deslogar</button>
        </li>
      </ul>
    </nav>
    <transition mode="out-in">
      <router-view></router-view>
    </transition>
  </section>
</template>

<script>
export default {
  name:"Usuario",
  methods:{
    deslogar(){
      this.$store.dispatch("deslogarUsuario")
      this.$router.push("/")
    }
  }

}
</script>

<style >
    .usuario{
    display: grid;
    grid-template-columns: minmax(140px,200px) 1fr;
    max-width: 1200px;
    margin: 40px auto;
    grid-gap: 30px;
    padding: 20px;
  }
  @media screen and (max-width: 500px){
    .usuario{
      grid-template-columns: 1fr;
      margin: 20px auto;
      grid-gap: 20px;
      padding: 20px;
    }
  }


  .sidenav a {
    padding: 10px;
    display: block;
    background: #f4f7fc;
    margin-bottom: 10px;
    border-radius: 4px;
  }

  .sidenav a.router-link-exact-active{
    background: #87f;
    color: #fff;
  }
  .sidenav button{
    padding: 10px;
    border: none;
    font-size: 1rem;
    width: 100%;
    text-align: left;
    font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
    cursor: pointer;
  }
</style>
