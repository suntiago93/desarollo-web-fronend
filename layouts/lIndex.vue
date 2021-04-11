<template>
  <v-app >
    <nuxt/>
    
     <v-footer :absolute="!fixed" color="rgb(162, 157, 156 , 0.5)" app>
           <center >
    <v-row>
    <v-col>
        <h3><strong>acerca de </strong> </h3>
        <v-btn  class="text-none" color="black"   plain to="#servicios"><small> Politica de privacidad</small> </v-btn>
        <br>
       <v-btn  class="text-none" color="black"  plain to="#contacto"> <small> Condiciones de uso</small> </v-btn>
       <br>
       <v-btn  class="text-none" color="black"  plain to="#contacto"> <small> Creditos</small> </v-btn>
    </v-col>
    <v-col>
        <h3><strong>opiniones </strong></h3>
        <v-btn  class="text-none" color="black"   plain to="#servicios"><small> Lo que dicen nuestros clientes</small> </v-btn>
    </v-col>
</v-row>
           </center>
           <v-row>
    <div style="width:1350px"><v-divider></v-divider></div>
        <span> &copy; {{ new Date().getFullYear() }} TuHábitat Inc. Todos los derechos reservados</span>
</v-row>
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