<template>
  <div>
    <NavBar :logo="logo_src" :alt="app_name"/>
  <router-view/>
  <Footer />
  </div>
  
</template>

<script>
  import NavBar from './components/NavBar.vue';
  import Footer from './components/Footer.vue'

  export default {
    name:'App',
    components:{
      NavBar,
      Footer
    },
    data(){
      return {
        logo_src: '/img/logo.png',
        app_name: 'Make Your Burger'
      }
    }
  }
</script>

<style>
*{
  font-family: Arial, Helvetica, sans-serif;
  padding: 0;
  margin:0;
  box-sizing: border-box;

}

.main-container{
  min-height: 250px;
  margin: 50px;
}

h1{
  text-align: center;
  font-size: 42px;
  margin-bottom: 30px;
  color: #222;
}
</style>
