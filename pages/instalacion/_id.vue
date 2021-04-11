<template>

<v-container >
    <div style="margin-top:2%">
    <h2 style="color:rgb(30, 181,181, 0.9)">Edicion de instalacion</h2>
    <div style="margin-left:80%">
    <v-btn
            :disabled="!valid"
            color="rgb(30, 181,181, 0.3)"
            class="text-none"
            to="/instalacion"
            rounded
            >
            ver registro
            </v-btn>
            </div>
<v-form ref="formularioInstalacion" v-model="valid" lazy-validation> 
 
 <v-text-field
            v-model="instalacion.id"
            :rules="regla.obligatorio"
            label="Id"
            :disabled="valid"
          ></v-text-field>
          <v-text-field
            v-model="instalacion.nombre"
            :rules="regla.obligatorio"
            label="Nombre"
            required
          ></v-text-field>
 <v-text-field
            v-model="instalacion.capacidad"
            :rules="regla.obligatorio"
            label="Capacidad"
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
            editar instalacion
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
      let id_instalacion=params.id;
      return {id_instalacion}
    },
   data: () => ({
      valid: true,
      instalacion:{},
      regla:{
          obligatorio:[ v => !!v || ' Is required'],
      },
     
   }),
    beforeMount(){
      this.getInstalacion();
    },
   methods: {
      async getInstalacion()
      {
          try {
            let response= await this.$axios.get('http://localhost:3001/instalacion/' + this.id_instalacion );
            console.log(response);
            this.instalacion=response.data
          } catch (error) {
             this.$swal(" error");
          }
        
      },
    
      async editar () {
        if (this.$refs.formularioInstalacion.validate()) {
              let instalacion=Object.assign({},this.instalacion);
            let response= await this.$axios.put('http://localhost:3001/instalacion/' + this.id_instalacion,instalacion);
            console.log(response +"respuesta");
            this.$swal("La edicion se realizo con exito");
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
