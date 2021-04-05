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
    <v-btn  class="text-none" color="white"   plain > configuracion </v-btn>
       <v-btn  class="text-none" color="white"  plain > herramientas </v-btn>
       <v-spacer></v-spacer>
      <v-btn  class="text-none" color="grey" rounded to="/login" > Iniciar sesion </v-btn>
    
    </v-app-bar>  


<v-main>
<v-container fluid>
    <div style="margin-top:2%">
    <h3>Formulario para registrar a los usuarios</h3>
    
<v-form ref="formularioUsuario" v-model="valid" lazy-validation> 
 
 <v-text-field
            v-model="usuario.id"
            :rules="regla.obligatorio"
            label="Id"
            required
          ></v-text-field>
          <v-text-field
            v-model="usuario.nombre"
            :rules="regla.obligatorio"
            label="Nombre"
            required
          ></v-text-field>
 <v-text-field
            v-model="usuario.apellido"
            :rules="regla.obligatorio"
            label="Apellido"
            required
          ></v-text-field>
 <v-text-field
            v-model="usuario.email"
            :rules="regla.email"
            label="Email"
            required
          ></v-text-field>
          <v-text-field
            v-model="usuario.clave"
            :rules="regla.obligatorio"
            label="Clave"
            required
          ></v-text-field>
 <v-text-field
            v-model="usuario.telefono"
            :rules="regla.obligatorio"
            label="Telefono"
            required
          ></v-text-field>
          
          <v-row
          width="100px">
          <v-col>
 <v-btn
            :disabled="!valid"
            color="rgb(30, 181,181, 0.3)"
            class="text-none"
            to="listaUsuario"
            rounded
            outline
            >
            Mostrar usuarios
            </v-btn>
          </v-col>
<v-fab-transition>
              <v-btn
                color="rgb(30, 181,181, 0.9)"
                dark
                absolute
                bottom
                right
                fab
                @click="agregar()"
              >
                <v-icon>mdi-plus</v-icon>
              </v-btn>
            </v-fab-transition>
                        
</v-row>
</v-form>
</div>
 
</v-container>
</v-main>
</v-app>
</template>



<script>

export default {
   data: () => ({
      valid: true,
      usuario:{id:"",nombre:"",apellido:"",email:"",clave:"",telefono:""},
      regla:{
          obligatorio:[ v => !!v || ' Is required'],
          email:[v => /.+@.+\..+/.test(v) || 'E-mail  be valid'],
      },
     
   }),
    
   methods: {
     async agregar () {
          if (this.$refs.formularioUsuario.validate()) {
              let usuario=Object.assign({},this.usuario);
            let response= await this.$axios.post('http://localhost:3001/usuario',usuario)
          }
          else{
            console.log("mal ");
          }      
      },

      editar () {
        this.$refs.form.reset()
      },
      borrar () {
        this.$refs.form.resetValidation()
      },
      actualizar () {
        this.$refs.form.resetValidation()
      },
      async getUsuario()
      {
         let response= await this.$axios.get('http://localhost:3001/usuario')
            console.log(response);
      }


    },
    }

</script>
