<template>
  <div id="app" class="conteiner-fluid">
    <b-nav-bar />
    <br />
    <div class="container-fluid">    
        <router-view/>    
    </div>
  </div>
</template>

<script>
import BNavBarVue from './components/BNavBar.vue';

export default {
  name: 'App',

  components:{
    'b-nav-bar':BNavBarVue
  }
}
</script>

<style>
#app {
  margin-left: 0%;
  margin-right: 0%;
}
</style>
