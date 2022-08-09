<template>
    <NavBar :logo="logo_src" :alt="alt_name"/>
    <router-view />
    <Footer />
</template>

<script>
import NavBar from './components/NavBar.vue'
import Footer from './components/Footer.vue'

export default {
  components: {
    NavBar,
    Footer
  },
  data(){
    return {
      logo_src: '/img/logo.png',
      alr_name: 'HomeTech'
    }
  }
}
</script>


<style>

  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: sans-serif;
  }
  body {
    background-color: #272727;
    
  }

  .main-container {
    margin: 50px;
    min-height: 250px;
  }

  h1 {
    font-size: 40px;
    text-align: center;
    margin-bottom: 20px;
    color: white;
  }
</style>
