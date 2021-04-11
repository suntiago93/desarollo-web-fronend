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
      

       <v-row>
        <v-col>
<v-dialog
        ref="dialogHoraInicio"
        v-model="modal3"
        :return-value.sync="time"
        persistent
        width="290px"
      >
        <template v-slot:activator="{ on, attrs }">
          <v-text-field
            v-model="reserva.horaIngreso"
            label="Desde"
            prepend-icon="mdi-clock-time-four-outline"
            readonly
            v-bind="attrs"
            v-on="on"
          ></v-text-field>
        </template>
        <v-time-picker
          v-if="modal3"
          v-model="reserva.horaIngreso"
          full-width
        >
          <v-spacer></v-spacer>
          <v-btn
            text
            color="primary"
            @click="modal3 = false"
          >
            Cancel
          </v-btn>
          <v-btn
            text
            color="primary"
            @click="$refs.dialogHoraInicio.save(time)"
          >
            OK
          </v-btn>
        </v-time-picker>
      </v-dialog>
        </v-col>

        <v-col>
<v-dialog
        ref="dialogHoraSalida"
        v-model="modal4"
        :return-value.sync="time1"
        persistent
        width="290px"
      >
        <template v-slot:activator="{ on, attrs }">
          <v-text-field
            v-model="reserva.horaSalida"
            label="Hasta"
            prepend-icon="mdi-clock-time-four-outline"
            readonly
            v-bind="attrs"
            v-on="on"
          ></v-text-field>
        </template>
        <v-time-picker
          v-if="modal4"
          v-model="reserva.horaSalida"
          full-width
        >
          <v-spacer></v-spacer>
          <v-btn
            text
            color="primary"
            @click="modal4 = false"
          >
            Cancel
          </v-btn>
          <v-btn
            text
            color="primary"
            @click="$refs.dialogHoraSalida.save(time1)"
          >
            OK
          </v-btn>
        </v-time-picker>
      </v-dialog>
        </v-col>
      
      </v-row>
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

       time: null,
        menu3: false,
        modal3: false,

        time1: null,
        menu4: false,
        modal4: false,
      valid: true,
      reserva:{},
      area: ['Piscina', 'Gimnacio', 'Cuarto de eventos', 'Cuarto de estudio'],
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
