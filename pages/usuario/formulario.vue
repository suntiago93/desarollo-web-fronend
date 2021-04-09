<template>

<v-container >
    <div style="margin-top:2%">
    <h3>Formulario para registrar usuarios</h3>
    
<v-form ref="formularioUsuario" v-model="valid" lazy-validation> 
 
 <v-text-field
            v-model="usuario.id"
            :rules="regla.obligatorio"
            label="Id"
            required
            clearable
          ></v-text-field>
          <v-text-field
            v-model="usuario.nombre"
            :rules="regla.obligatorio"
            label="Nombre"
            required
            clearable
          ></v-text-field>
 <v-text-field
            v-model="usuario.apellido"
            :rules="regla.obligatorio"
            label="Apellido"
            required
            clearable
          ></v-text-field>
  <v-text-field
            v-model="usuario.telefono"
            :rules="regla.obligatorio"
            label="Telefono"
            required
            clearable
          ></v-text-field>     
  <v-text-field
            v-model="usuario.apartamento"
            :rules="regla.obligatorio"
            label="Apartamento"
            required
            clearable
          ></v-text-field>            
 <v-text-field
            v-model="usuario.email"
            :rules="regla.email"
            label="Email"
            required
            clearable
          ></v-text-field>
          <v-text-field
            v-model="usuario.clave"
            :rules="regla.obligatorio"
            label="Clave"
            required
            clearable
          ></v-text-field>

          
          <v-row
          width="100px">
          <v-col>
 <v-btn
            
            color="rgb(30, 181,181, 0.3)"
            class="text-none"
            to="/usuario"
            rounded
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

</template>



<script>

export default {
  
   data: () => ({
      valid: true,
      usuario:{id:"",nombre:"",apellido:"",telefono:"",apartamento:"",email:"",clave:""},
      regla:{
          obligatorio:[ v => !!v || ' Is required'],
          email:[v => /.+@.+\..+/.test(v) || 'E-mail  be valid'],
      },
     
   }),
    beforeMount(){},
   methods: {
     async agregar () {
          if (this.$refs.formularioUsuario.validate()) {
              let usuario=Object.assign({},this.usuario);
            let response= await this.$axios.post('http://localhost:3001/usuario',usuario);
            this.$swal("agregado");  
          }
          else{
            console.log("mal ");
          }      
      },

     
      async getUsuario()
      {
         let response= await this.$axios.get('http://localhost:3001/usuario')
            console.log(response);
      }


    },
    }

</script>
