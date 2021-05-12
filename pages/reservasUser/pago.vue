<!-- obener fecha [new Date().toISOString().substr(0, 10)]  -->

<template>
<v-row justify="center" align="center">
        <v-col cols="12">
            <v-card flat color="rgb(8, 239, 247)">
              <h1 style="text-align:center; color:grey"> lista de reservas a pagar</h1>
              <v-card-actions>
                <v-spacer></v-spacer>
              </v-card-actions>


  <v-data-table
    v-model="selected"
    :single-select="singleSelect"
    item-key="id"
    show-select
    :headers="headers"
    :items="reservas"
    sort-by="fecha"
    class="green lighten-4"
  >
    <template v-slot:top>
      <v-toolbar
        flat
        class="green lighten-4"
      >
        <v-toolbar-title >Efectue su pago facilmente</v-toolbar-title>
        <v-divider
          class="mx-4"
          inset
          vertical
        ></v-divider>
        <v-spacer></v-spacer>
        <v-dialog
          v-model="dialog"
          max-width="700px"
        >
        
          <v-card>
            <v-card-title>
             
            </v-card-title>

            <v-card-text>
              <v-container>
            <v-row>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Documento de identidad"
                  required
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Nombre"
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Apellido"
                  required
                ></v-text-field>
              </v-col>
              <v-col cols="12"
                sm="6"
                
              >
                <v-select
                  :items="['visa', 'master-card', 'american express']"
                  label="Tarjeta"
                  required
                ></v-select>
              </v-col>
               <v-col cols="12"
               sm="6"
                >
                <v-text-field
                  label="Fecha de vencimiento"
                  
                  required
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  label="Numero de tarjeta"
                  type="number"
                  required
                ></v-text-field>
              </v-col>
            </v-row>
          </v-container>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                color="blue darken-1"
                text
                @click="close"
              >
                Cancelar
              </v-btn>
              <v-btn
                color="blue darken-1"
                text
                @click="save"
              >
                pagar
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-toolbar>
    </template>
    <template v-slot:item.actions="{ item }">
      <v-icon
        large
        class="mr-2"
        @click="editItem(item)"
      >
        mdi-credit-card-outline
      </v-icon>
     
    </template>
   
  </v-data-table>
  
  </v-card>
  
  </v-col>
  <v-spacer></v-spacer>
  <v-btn rounded color="rgb(8, 120, 247, 0.575)"  block class="text-none; " @click="Pagar()">Pagar todas las reservas</v-btn>
  </v-row>  
  
</template>

<script>
  export default {
     layout:"lHomeUser",
    data: () => ({
      dialog: false,
      singleSelect: false,
        selected: [],
      
      headers: [
        {
          text: 'Id',
          align: 'start',
          value: 'id',
        },
        { text: 'Fecha de reserva', value: 'fechaReserva' },
        { text: 'sector', value: 'sector' },
        { text: 'precio', value: 'precio' },
        { text: 'Aciones', value: 'actions'},
      ],
      reservas: [ 
        {
            id: '1',
            fechaReserva: 159,
            sector: 6.0,
            precio: 24,
          },

          {
            id: '21',
            fechaReserva: 159,
            sector: 6.0,
            precio: 24,
          },
      ],
      
      
    }),

    methods: {
    
      editItem (item) {
        
        this.dialog = true
      },

      save()
      {
        this.dialog=false;
      },

       close()
      {
        this.dialog=false;
      }

     
    },
  }
</script>

