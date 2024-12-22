<template>
  <nav>
    <!-- -->
    <!--<router-link to="/">Vue </router-link>| -->
    <router-link to="/contacto">Contactos</router-link>|
    <router-link to="/about">Integrante</router-link>
    
    
    <!--<router-link to="/parqueo">Parqueo</router-link>|-->
    
  </nav>




  <router-view/> 
</template>




<script>
import ContactoView from './views/ContactoView.vue'

export default {
  components: {
    ContactoView
  }
}

</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #D1510F;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #D1510F;

    &.router-link-exact-active {
      color: #D1510F;
    }
  }
}
</style>
