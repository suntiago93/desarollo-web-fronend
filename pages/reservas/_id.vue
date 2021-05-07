<template>

<v-container >
    <div style="margin-top:2%">
    <h2 style="color:rgb(30, 181,181, 0.9)">Editar reserva</h2>
    <div style="margin-left:80%">
     <v-btn 
            color="rgb(30, 181,181, 0.3)"
            class="text-none"
            to="/reservas"
            rounded
            
            >
            Mostrar Reservas
            </v-btn>
            </div>
<v-form ref="formularioReserva" v-model="valid" lazy-validation> 
 

 <v-text-field
            v-model="reserva.id"
            :rules="regla.obligatorio"
            label="Id"
            :disabled="valid"
            prepend-icon="mdi-account-outline"
          ></v-text-field>
           <v-select
           v-model="reserva.sector"
          :items="area"
          label="Sector"
          prepend-icon="mdi-city"
          :rules="regla.obligatoria"
          required
        ></v-select>
        <v-dialog
        ref="dialogFecha"
        v-model="modal"
        :return-value.sync="date"
        persistent
        width="290px"
      >
        <template v-slot:activator="{ on, attrs }">
          <v-text-field
            v-model="reserva.fecha"
            label="Fecha"
            prepend-icon="mdi-calendar"
            readonly
            v-bind="attrs"
            v-on="on"
          ></v-text-field>
        </template>
        <v-date-picker
          v-model="reserva.fecha"
          scrollable
        >
          <v-spacer></v-spacer>
          <v-btn
            text
            color="primary"
            @click="modal = false"
          >
            Cancel
          </v-btn>
          <v-btn
            text
            color="primary"
            @click="$refs.dialogFecha.save(date)"
          >
            OK
          </v-btn>
        </v-date-picker>
      </v-dialog>
      
<v-select
          v-show="reserva.sector == 'Piscina'"
          v-model="reserva.hora"
          :items="rangoHorarioPiscina"
          label="Rango de horario"
          prepend-icon="mdi-clock-time-four-outline"
          :rules="regla.obligatoria"
          required
        ></v-select>

         <v-select
         v-show="reserva.sector == 'Gimnacio'"
           v-model="reserva.hora"
          :items="rangoHorarioGimnacio"
          label="Rango de horario"
          prepend-icon="mdi-clock-time-four-outline"
          :rules="regla.obligatoria"
          required
        ></v-select>
         <v-select
         v-show="reserva.sector == 'Cuarto de eventos'"
           v-model="reserva.hora"
          :items="rangoHorarioEvento"
          label="Rango de horario"
          prepend-icon="mdi-clock-time-four-outline"
          :rules="regla.obligatoria"
          required
        ></v-select>
         <v-select
         v-show="reserva.sector == 'Cuarto de estudio'"
           v-model="reserva.hora"
          :items="rangoHorarioEstudio"
          label="Rango de horario"
          prepend-icon="mdi-clock-time-four-outline"
          :rules="regla.obligatoria"
          required
        ></v-select>
       
              <v-btn
                color="rgb(30, 181,181, 0.9)"
                right 
                rounded
                @click="editar()"
              >
               editar
              </v-btn>
</v-form>
</div>
 
</v-container>

</template>



<script>

export default {
  
  async asyncData({ params }) {
      let id_reserva=params.id;
      return {id_reserva}
    },
   data: () => ({
      date: new Date().toISOString().substr(0, 10),
      menu: false,
      modal: false,
      menu2: false,
      valid: true,
      reserva:{},
      area: ['Piscina', 'Gimnacio', 'Cuarto de eventos', 'Cuarto de estudio'],
      rangoHorarioPiscina: ['8:00 hs - 12:00 hs', '12:00 hs - 16:00 hs', '16:00 hs - 20:00 hs'],
      rangoHorarioGimnacio: ['8:00 hs - 10:00 hs', '10:00 hs - 12:00 hs', '12:00 hs - 14:00 hs', '14:00 hs - 16:00 hs', '16:00 hs - 18:00 hs', '18:00 hs - 20:00 hs'],
      rangoHorarioEvento: ['8:00 hs - 13:00 hs', '13:00 hs - 18:00 hs', '18:00 hs - 23:00 hs'],
      rangoHorarioEstudio: ['8:00 hs - 11:00 hs', '11:00 hs - 14:00 hs', '14:00 hs - 17:00 hs' , '17:00 hs - 20:00 hs'],
      regla:{
          obligatorio:[ v => !!v || ' Is required'],
          email:[v => /.+@.+\..+/.test(v) || 'E-mail  be valid'],
      },
     
   }),
    beforeMount(){
      this.getReserva();
    },
   methods: {
      async getReserva()
      {
          try {
            let response= await this.$axios.get('http://localhost:3001/reserva/' + this.id_reserva );
            console.log(response);
            this.reserva=response.data
          } catch (error) {
             this.$swal(" error");
          }
        
      },
    
      async editar () {
        if (this.$refs.formularioReserva.validate()) {
              let reservas=Object.assign({},this.reserva);
            let response= await this.$axios.put('http://localhost:3001/reserva/' + this.id_reserva,reservas);
            this.$swal(" La edicion fue realizada con exito");
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
