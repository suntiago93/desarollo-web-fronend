<template>

<v-container >
    <div style="margin-top:2%">
    <h2 style="color:rgb(30, 181,181, 0.9)">Formulario para registrar usuarios</h2>
    
<v-form ref="formularioUsuario" v-model="valid" lazy-validation> 
 <div style="margin-left:80%"> <v-btn     
            color="rgb(30, 181,181, 0.3)"
            class="text-none"
            to="/usuario"
            rounded
            >
            Mostrar usuarios
            </v-btn>
 </div>
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
           <v-select
           v-model="usuario.parqueadero"
          :items="parqueadero"
          label="Parqueadero"
          :rules="regla.obligatoria"
          required
        ></v-select>  
        <v-text-field
            v-show="usuario.parqueadero == 'Si'"
            v-model="usuario.numParqueadero"
            :rules="regla.obligatoria"
            label="Numero parqueadero"
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

          <v-select
           v-model="usuario.rol"
           :items="roles"
           item-value="id"
           item-text="nombre"
           label="rol"
           :rules="regla.obligatoria"
           required
        ></v-select>
<div style="height:80px;">
<v-btn
                color="rgb(30, 181,181, 0.9)"
                dark
                bottom
                right 
                @click="agregar()"
              >
                <v-icon>mdi-plus</v-icon>
              </v-btn>
              </div>
</v-form>
</div>
 
</v-container>

</template>



<script>

export default {
  
   data: () => ({
      valid: true,
      usuario:{id:"",nombre:"",apellido:"",telefono:"",apartamento:"",parqueadero:"",numParqueadero:"",email:"",clave:""},
      parqueadero: ['Si', 'No'],
       roles: [ {id:1,nombre:'administrador'},
                {id:2,nombre:'usuario'} ,
                {id:3,nombre:'invitado'},
                {id:1,nombre:'otro'}
        ],
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
            this.$swal("El proceso de registro finalizo con exito");  
            this.$refs.formularioUsuario.reset();
          }
          else{
            console.log("Ups hubo un error");
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
