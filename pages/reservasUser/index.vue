<template>

   <v-row justify="center" align="center">
        <v-col cols="12">
            <v-card flat color="rgb(8, 239, 247)">
              <h1 style="text-align:center; color:rgb(30, 181,181, 0.9)"> lista de reservas usuarios</h1>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn rounded color="rgb(30, 181,181, 0.9)" class="text-none; " @click="registrarReserva()">Registrar reserva</v-btn>
              </v-card-actions>
        
              <v-data-table
                :headers="headers"
                :items="reserva"
                :items-per-page="5"
                class="green lighten-4"
                
                >
                <template v-slot:item.actions="{ item }">
      <v-icon
        small
        class="mr-2"
        @click="editItem(item)"
      >
        mdi-pencil
      </v-icon>
      <v-icon
        small
        @click="deleteItem(item)"
      >
        mdi-delete
      </v-icon>

    </template>
             </v-data-table>
            </v-card>

        </v-col>
    </v-row>  



    
</template>

<script>
  export default {

    layout:"lHomeUser",
    
      beforeMount(){
          this.getReserva();
      },
    data () {
      return {
        headers: [
          {
            text: 'id',
            align: 'start',
            value: 'id',
          },
          { text: 'Fecha', value: 'fecha'},
          { text: 'Sector', value: 'sector' },
          { text: 'Horario', value: 'hora' },
          { text: 'Acción', value: 'actions' }
        ],
        reserva: [],
      };
    },
        methods:{
             async getReserva()
      {
          try {
            let response= await this.$axios.get('http://localhost:3001/reserva')
            this.reserva=response.data;
          } catch (error) {
              
          }
        
      },
      
      editItem(item)
      {
        let url= "/reservasUser/" + item.id;
        this.$router.push(url)
      },
      deleteItem(item)
  {
   this.$swal.fire({
  type:"warning",
  title: '¿Seguro?',
  text: "vas a borrar un registro!",
  icon: 'warning',
  allowEscapeKey:false,
  allowOutsideClick:false,
  showCancelButton:true,
}).then(async(result) => {
  if (result.value) {
    try{
      let url='http://localhost:3001/reserva/' + item.id;
      let response= await this.$axios.delete(url);
      this.$swal.fire({
        type:"success",
        title:"operacion exitosa.",
        text:"el item se elimino correctamente"
      });
      this.getReserva();
    
    }catch (error){
      this.$swal.fire({
        type:"error",
        title:"ha ocurrido un problema al eliminar",
        text: error.toString(),
        });
       }
      }
    
    }
  );

  },
  registrarReserva(){
    let url= '/reservasUser/formulario';
        this.$router.push(url)
  }

  }
  }
</script>


 <style scoped>
.v-application {
    background-color:rgb(29, 212, 22)
}
</style>