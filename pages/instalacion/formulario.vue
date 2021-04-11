<template>

<v-container >
    <div style="margin-top:2%">
    <h2 style="color:rgb(30, 181,181, 0.9)">Formulario para registrar instalaciones</h2>
    <div style="margin-left:80%">
     <v-btn 
            color="rgb(30, 181,181, 0.3)"
            class="text-none"
            to="/instalacion"
            rounded
            >
            Mostrar instalaciones
            </v-btn>
            </div>
    
<v-form ref="formularioInstalacion" v-model="valid" lazy-validation> 
 
 <v-text-field
            v-model="instalacion.id"
            :rules="regla.obligatorio"
            label="Id"
            required
            clearable
          ></v-text-field>
          <v-text-field
            v-model="instalacion.nombre"
            :rules="regla.obligatorio"
            label="Nombre"
            required
            clearable
          ></v-text-field>
 <v-text-field
            v-model="instalacion.capacidad"
            :rules="regla.obligatorio"
            label="capacidad"
            required
            clearable
          ></v-text-field> 
           <v-btn
                color="rgb(30, 181,181, 0.9)"
                dark
                bottom
                right 
                @click="agregar()"
              >
                <v-icon>mdi-plus</v-icon>
              </v-btn>
</v-form>
</div>
 
</v-container>

</template>



<script>

export default {
  
   data: () => ({
      valid: true,
      instalacion:{id:"",nombre:"",capacidad:""},
      regla:{
          obligatorio:[ v => !!v || ' Is required'],
      },
     
   }),
    beforeMount(){},
   methods: {
     async agregar () {
          if (this.$refs.formularioInstalacion.validate()) {
              let instalacion=Object.assign({},this.instalacion);
            let response= await this.$axios.post('http://localhost:3001/instalacion',instalacion);
            this.$swal("El proceso de registro finalizo con exito");  
            this.$refs.formularioInstalacion.reset();
          }
          else{
             this.$swal("Ups hay un error, verifique si no existe el ese registro con el mismo id");
          }      
      },

     
      async getInstalacion()
      {
         let response= await this.$axios.get('http://localhost:3001/usuario')
            console.log(response);
      }


    },
    }

</script>
