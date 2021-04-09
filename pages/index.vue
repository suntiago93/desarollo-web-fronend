<template>
      <v-app>
    <v-app-bar
      app
      color="black"
    >
        <!-- Titulo barra de vavegacion -->
      <v-toolbar-title class="white--text"> TuHabitat </v-toolbar-title >
      <v-spacer></v-spacer>
    <!-- Botones barra de navegacion -->
    <v-btn  class="text-none" color="white"   plain to="#servicios"> servicios </v-btn>
       <v-btn  class="text-none" color="white"  plain to="#contacto"> contactanos </v-btn>
       <v-spacer></v-spacer>
      <v-btn  class="text-none" color="grey" rounded to="/login" > Iniciar sesion </v-btn>
    
    </v-app-bar>  
    
    
<v-main>
  <v-container fluid>
      <!-- Carrucel con imagenes -->
    <div class="images">
      <Hero/>
    </div >
      <!-- Titulo de bajo carrucel -->
    <div>
      <h2 id="title">somos una alternativa</h2>
      </div> 
      <!-- Separador -->
      <div style="width:100px; height:90px;" id="servicios"> </div>
      <!-- Segundo titulo -->
      <div><h1 class="black--text text--lighten-9" ><strong >Realizar cualquier transaccion sin salir de casa</strong></h1></div>
      <!-- Separador -->
  <div style="width:100px; height:30px;"> </div>

  <!-- fila con imagenes y titulo servicios -->
  <div >
  <v-row>
    <v-col>
      <v-card
    class="mx-auto"
    max-width="300"
    height="400px"
  >
    <v-img
      class="white--text align-end"
      height="400px"
      :src="require('../assets/images/reserva-web.jpg')"
    >
    </v-img>
    <v-card-subtitle class="pb-0"><h2 style="text-align: center;"> Reserva establecimientos</h2></v-card-subtitle>
  </v-card>
    </v-col>



    <v-col>
      <v-card
    class="mx-auto"
    max-width="300"
    height="400px"
  >
    <v-img
      class="white--text align-end"
      height="400px"
      :src="require('../assets/images/pago.png')"
    >
    </v-img>
    <v-card-subtitle class="pb-0"><h2 style="text-align: center;"> Realiza pagos</h2></v-card-subtitle>
  </v-card>
    </v-col>


    <v-col>
      <v-card
    class="mx-auto"
    max-width="300"
    height="400px"
  >
    <v-img
      class="white--text align-end"
      height="400px"
      :src="require('../assets/images/archivo.jpg')"
    >
    </v-img>
    <v-card-subtitle class="pb-0"><h2 style="text-align: center;"> Consultas facturas y mas</h2></v-card-subtitle>
  </v-card>
    </v-col>
  </v-row>
  </div>
  


  <!-- Separador -->
<div style="width:800px; height:120px;"> </div>
 

<!-- Tarjeta contacto -->
<div style=" text-align:center;" id="contacto">
  <v-card
      class="d-flex justify-center mb-6"
      flat
      tile
    >
      <v-card
        class="pa-2"
        outlined
        tile
      >
         <v-img
      class="white--text align-end"
      height="600px"
      width="1200px"
      :src="require('../assets/images/unidadResidencial.png')"
    >
    <v-row>
      <v-col>
       <div style=" height:400px;" > 
         <h1>Accede a mas informacion</h1>
         <h3>______________________________________________ </h3>
         <p>Mantente al tanto de nuestras ofertas,
           <br> nuestras actualizaciones <br> y familiarzate mas con nuestro servicio.</p>
       </div>
      </v-col>
      <v-col>
       <div> 
        
    
    
      <v-card
        class=" pa-2; ma-2 red--text text--lighten-1 d-flex justify-center mb-6"
        outlined
        tile
        width="350"
        height="250"
        text-align:center;
        color="rgb(0, 0, 0, 0.5)"
      >
         <v-form
    ref="form"
    v-model="valid"
    lazy-validation
    class="mt-5"
    
  >
    <v-text-field
      v-model="name"
      :rules="nameRules"
      label="Nombre"
      required
      rounded-s
      
      
    ></v-text-field>

    <v-text-field
      v-model="email"
      :rules="emailRules"
      label="Email"
      required
      rounded-s
      
    ></v-text-field>
    <v-btn
      :disabled="!valid"
      color="rgb(251, 251, 251, 0.9)"
      class="mr-2 mt-2"
      
      width="220px"
      rounded
    
    >
    <strong >Enviar informacion</strong>
    </v-btn>
         </v-form>

      </v-card>
         </div>
      </v-col>
    </v-row>
    </v-img>
      </v-card>
  </v-card>
</div>
</v-container>


</v-main>
  
  </v-app>
   
  

</template>

<script>

import Hero from '~/components/Hero.vue'




export default {
  
  components: {
    Hero,
  },
   data: () => ({
      valid: true,
      name: '',
      nameRules: [
        v => !!v || 'Name is required',
       
      ],
      email: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
      ],
      }),

    methods: {
     
     
    },
}
</script>

<style>

#title{
    text-align: center;
}
#title2{
    text-align: start;
}
</style>
