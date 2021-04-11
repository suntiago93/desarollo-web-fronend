<template>
  <v-app >
    <nuxt/>
    
     <v-footer
      :absolute="!fixed"
      app
      padless
      color="rgb(162, 157, 156 , 0.5)"
    >
    <div > &copy; {{ new Date().getFullYear() }} TuHábitat Inc. Todos los derechos reservados</div>
    </v-footer>  
  </v-app>
  
</template>

<script>
export default {
  data () {
    return {
      fixed:false
      
    }
  }
}
</script>

<style>


</style>