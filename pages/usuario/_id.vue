<template>

<v-container >
    <div style="margin-top:2%">
    <h2 style="color:rgb(30, 181,181, 0.9)">Edicion de usuario</h2>
    <v-btn
            :disabled="!valid"
            color="rgb(30, 181,181, 0.3)"
            class="text-none"
            to="/usuario"
            rounded
            >
            ver registro
            </v-btn>
<v-form ref="formularioUsuario" v-model="valid" lazy-validation> 
 
 <v-text-field
            v-model="usuario.id"
            :rules="regla.obligatorio"
            label="Id"
            :disabled="valid"
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
            v-model="usuario.telefono"
            :rules="regla.obligatorio"
            label="Telefono"
            required
          ></v-text-field>     
  <v-text-field
            v-model="usuario.apartamento"
            :rules="regla.obligatorio"
            label="Apartamento"
            required
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
          ></v-text-field>
          <v-text-field
            v-model="usuario.clave"
            :rules="regla.obligatorio"
            label="Clave"
            required
          ></v-text-field>

          
          <v-row
          width="100px">
          <v-col>
 <v-btn
            :disabled="!valid"
            color="rgb(30, 181,181, 0.3)"
            class="text-none"
            @click="editar()"
            rounded
            >
            editar usuario
            </v-btn>
          </v-col>

                        
</v-row>
</v-form>
</div>
 
</v-container>

</template>



<script>

export default {
  
  async asyncData({ params }) {
      let id_usuario=params.id;
      return {id_usuario}
    },
   data: () => ({
      valid: true,
      usuario:{},
       parqueadero: ['Si', 'No'],
      regla:{
          obligatorio:[ v => !!v || ' Is required'],
          email:[v => /.+@.+\..+/.test(v) || 'E-mail  be valid'],
      },
     
   }),
    beforeMount(){
      this.getUsuario();
    },
   methods: {
      async getUsuario()
      {
          try {
               let response= await this.$axios.get('http://localhost:3001/usuario/' + this.id_usuario );
            console.log(response);
            this.usuario=response.data
          } catch (error) {
             this.$swal(" error");
          }
        
      },
    
      async editar () {
        if (this.$refs.formularioUsuario.validate()) {
              let usuario=Object.assign({},this.usuario);
            let response= await this.$axios.put('http://localhost:3001/usuario/' + this.id_usuario,usuario);
            console.log(response +"respuesta");
            this.$swal("se realizo con exito");
          }
          else{
            console.log("Ups hubo un error");
          }      
      },
      
      actualizar () {
        this.$refs.form.resetValidation()
      },
     


    },
    }

</script>
