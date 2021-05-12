
<template>
  <v-card flat >
    <v-tabs
      color="deep-purple accent-4"
      right
    >
      <v-tab>Usuario</v-tab>
      <v-tab>Reserva</v-tab>
      
 <v-tab-item>
   <v-container fluid>
     <v-row justify="center" align="center">
       <v-col cols="12">
        <v-card flat >
          <v-form ref="formularioConsula" v-model="valid" lazy-validation> 
            <center>
            <h1 style="color:black">
                Consultar informacion relacionada a los usuarios
            </h1>
            </center>
            <br/>
            <br/>
            <v-radio-group v-model="radioGroup">
            <v-row>
              
              <v-radio  value="opcion1"  ></v-radio>
            <h3> Consultar informacion sobre el usuario segun: </h3>
            </v-row>
            <br/>
            
            <v-select
             v-model="selector"
            :items="categorias"
            filled
            label="Categorias"
        ></v-select>
        <v-row>
          <v-col cols="12" sm="6">
            <v-text-field
            
             v-show="selector == 'Nombre & Apellido'"
            label="Nombre"
            required
            clearable
          ></v-text-field>
          </v-col>
         
          <v-col cols="12" sm="6">
          <v-text-field
           v-show="selector == 'Nombre & Apellido'"
          label="Apellido"
          required
          clearable
          ></v-text-field>
          </v-col>
        </v-row>
        <v-text-field
        v-show="selector == 'Id' || selector == 'Cedula'"
            required
            clearable
          ></v-text-field>
            <br />
            <v-row>
              <v-radio value="opcion2"></v-radio>
            <h3>  Cantitad de inmuebles ocupados </h3>
            </v-row>
            <br/>
            </v-radio-group>
            <v-select
            :items="roles"
            filled
            label="Rol"
        ></v-select>
        
            <br />
          
           <v-card-actions>
             <v-btn color="rgb(30, 181,181, 0.9)" class="text-none" dark bottom >
                 Consultar
                <v-divider
      class="mx-4"
      vertical
    ></v-divider>
                 <v-icon>mdi-magnify</v-icon>
             </v-btn>
           </v-card-actions>
          </v-form>
        </v-card>
         
       </v-col>
     </v-row>
   </v-container>
  </v-tab-item>
  


<v-tab-item>
   <v-container fluid>
     <v-row justify="center" align="center">
       <v-col cols="12">
        <v-card flat >
            <center>
            <h1 style="color:black">
                Consultar informacion relacionada a las reservas
            </h1>
            </center>
            <br/>
            <br/>
            <v-radio-group v-model="radioGroup">
            <v-row>
              <v-radio  value="opcion1"></v-radio>
            <h3> Consultar cantidad de reservar echas en un sector:</h3>
            </v-row>
            <br/>
            <v-select
             v-model="sector1"
            :items="sectores1"
            filled
            :rules="regla.obligatoria"
            label="sector"
        ></v-select>
            <br />
            <v-row>
              <v-radio value="opcion2"></v-radio>
            <h3> Disponibilidad de reserva una en una fecha, hora y sector </h3>
            </v-row>
            <br />
             <v-select
             v-model="sector2"
            :items="sectores2"
            filled
            label="sector"
            :rules="regla.obligatoria"
        ></v-select>
             <v-row>
          <v-col cols="12" sm="6">
            <v-dialog
        ref="dialogFecha"
        v-model="modal"
        :return-value.sync="date"
        persistent
        width="290px"
      >
        <template v-slot:activator="{ on, attrs }">
          <v-text-field
            v-model="fecha"
            label="Fecha"
            prepend-icon="mdi-calendar"
            readonly
            v-bind="attrs"
            v-on="on"
            required
            :rules="regla.obligatoria"
          ></v-text-field>
        </template>
        <v-date-picker
          v-model="fecha"
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
          </v-col>
         
          <v-col cols="12" sm="6">
         <v-select
          v-show="sector2 == 'Piscina'"
          v-model="hora"
          :items="rangoHorarioPiscina"
          label="Rango de horario"
          prepend-icon="mdi-clock-time-four-outline"
          :rules="regla.obligatoria"
          required
        ></v-select>

         <v-select
         v-show="sector2 == 'Gimnacio'"
           v-model="hora"
          :items="rangoHorarioGimnacio"
          label="Rango de horario"
          prepend-icon="mdi-clock-time-four-outline"
          :rules="regla.obligatoria"
          required
        ></v-select>
         <v-select
         v-show="sector2 == 'Cuarto de eventos'"
           v-model="hora"
          :items="rangoHorarioEvento"
          label="Rango de horario"
          prepend-icon="mdi-clock-time-four-outline"
          :rules="regla.obligatoria"
          required
        ></v-select>
         <v-select
         v-show="sector2 == 'Cuarto de estudio'"
           v-model="hora"
          :items="rangoHorarioEstudio"
          label="Rango de horario"
          prepend-icon="mdi-clock-time-four-outline"
          :rules="regla.obligatoria"
          required
        ></v-select>
          </v-col>
        </v-row>
            
            </v-radio-group>
           <v-card-actions>
             <v-btn color="rgb(30, 181,181, 0.9)" class="text-none" @click="consultar" dark bottom >
                 Consultar
                <v-divider
      class="mx-4"
      vertical
    ></v-divider>
                 <v-icon>mdi-magnify</v-icon>
             </v-btn>
           </v-card-actions>
        </v-card>
       </v-col>
     </v-row>
   </v-container>     
       

      </v-tab-item> 
    </v-tabs>
  </v-card>
</template>


<script>
export default {
    layout:"lHome",
data: () => ({
  valid: true,
  regla:{
          obligatorio:[ v => !!v || ' Is required'],
  },
  categorias: ['Id', 'Cedula','Nombre & Apellido'],
  roles: ['Propietario', 'administrador'],
  sectores: ['Piscina', 'Gimnacio', 'Cuarto de eventos', 'Cuarto de estudio'],
  sectores1: ['Piscina', 'Gimnacio', 'Cuarto de eventos', 'Cuarto de estudio'],
  sectores2: ['Piscina', 'Gimnacio', 'Cuarto de eventos', 'Cuarto de estudio'],
  rangoHorarioPiscina: ['8:00 hs - 12:00 hs', '12:00 hs - 16:00 hs', '16:00 hs - 20:00 hs'],
  rangoHorarioGimnacio: ['8:00 hs - 10:00 hs', '10:00 hs - 12:00 hs', '12:00 hs - 14:00 hs', '14:00 hs - 16:00 hs', '16:00 hs - 18:00 hs', '18:00 hs - 20:00 hs'],
  rangoHorarioEvento: ['8:00 hs - 13:00 hs', '13:00 hs - 18:00 hs', '18:00 hs - 23:00 hs'],
  rangoHorarioEstudio: ['8:00 hs - 11:00 hs', '11:00 hs - 14:00 hs', '14:00 hs - 17:00 hs' , '17:00 hs - 20:00 hs'],
  selector:"",
  selector:"",
  fecha:"",
  sector:null,
  sector1:null,
  sector2:null,
  radioGroup:"opcion1",
   date: new Date().toISOString().substr(0, 10),
      menu: false,
      modal: false,
      menu2: false,


}),
methods:{
  consultar(){
     if (this.$refs.formularioReserva.validate()) {
     }
  }
}
}

</script>

<style>

</style>