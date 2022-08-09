<template>
  <div>
    <div class="main-container">
        <h1>Gerenciar serviços:</h1>
        <Dashboard />
    </div>   
  </div>
</template>


<script>

import Dashboard from '../components/Dashboard.vue'

export default {
  name: 'Servicos',
  components : {
    Dashboard
  }
}
</script>


<style scoped>
  
</style>