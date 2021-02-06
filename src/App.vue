<template>
  <div id="app">
    <TheHeader/>
    <main id="main">
      <transition mode="out-in">
        <router-view/>
      </transition>
    </main>
    <TheFooter/>
  </div>
</template>

<script>
import TheHeader from './components/TheHeader'
import TheFooter from './components/TheFooter'

export default {
  name: 'App',
  components: {
    TheHeader,
    TheFooter,

  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@300&display=swap');

#app{
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

label{
  margin-bottom: 5px;
}

input,textarea{
  border-radius: 4px ;
  border: 1px solid #fff;
  padding: 15px;
  box-shadow: 0 4px 8px rgba(30,60,90,.2);
  transition: all .3s;
  font-size: 1rem;
  font-family: 'Open Sans';
  margin-bottom: 15px;
}

input:hover,
input:focus,
textarea:hover,
textarea:focus{
  outline: none;
  box-shadow: 0 6px 12px rgba(30,60,90,.2);
  border-color: #87f;
}

*{
  box-sizing: border-box;
}

body,ul,li,h1,h2,p{
  margin: 0px;
  padding: 0px;
}

ul{
  list-style: none;
}

body{
  font-family: 'Open Sans';
  color: #345;
  background: url('./assets/pattern.svg') repeat top;
}

a{
  color: #345;
  text-decoration: none;
}

img{
  max-width: 100%;
  display: block;
}

.btn{
  display: block;
  padding: 10px 30px;
  background: #87f;
  border-radius: 4px;
  color: white;
  box-shadow: 0px 4px 8px rgba(30,60,90,0.2);
  text-align: center;
  transition: all 1s;
  border: none;
  font-family: 'Open Sans';
  cursor: pointer;
}

.btn:hover{
  background: #65d;
  transform: scale(1.1);
}

#main{
  flex: 1;
}

.v-enter,
.v-leave-to{
  opacity: 0;
}

.v-enter{
  transform: translate3d(0,-20px, 0);
}

.v-enter-to{
  transform: translate3d(0,20px);
}

.v-enter-active, .v-leave-active {
  transition: all 0.3s;
}

</style>
