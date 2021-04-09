<template>
  <v-app >
    <nuxt/>
    <v-footer
      :absolute="!fixed"
      app
      padless
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