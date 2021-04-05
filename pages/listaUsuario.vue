<template>
<div style="text-align:center;">
   <v-row justify="center" align="center">
        <v-col cols="12">
            
            <v-card >
                <h1 style="text-align: center" >Lista de usuarios</h1>
                <v-spacer></v-spacer>
            <div style="margin-left:85%">
                 <v-btn rounded color="rgb(30, 181,181, 0.9)" class="text-none" to="/usuario">Registrar usuario</v-btn>
            </div>
            <v-spacer></v-spacer>
              <v-data-table
                :headers="headers"
                :items="usuario"
                :items-per-page="5"
                class="elevation-1"
                >
               
             </v-data-table>
            </v-card>

        </v-col>
    </v-row>  
    
</div>

    
</template>

<script>
  export default {
      beforeMount(){
          this.getUsuario();
      },
    data () {
      return {
        headers: [
          {
            text: 'Id',
            align: 'start',
            value: 'id',
          },
          { text: 'Nombre', value: 'nombre' },
          { text: 'Apellido', value: 'apellido' },
          { text: 'Email', value: 'email' },
          { text: 'Clave', value: 'clave' },
          { text: 'Telefono', value: 'telefono' },
          { text: 'Acción', value: 'accion' },
        ],
        usuario: [],
      };
    },
        methods:{
             async getUsuario()
      {
          try {
               let response= await this.$axios.get('http://localhost:3001/usuario')
            this.usuario=response.data;
          } catch (error) {
              
          }
        
      }

        }
  }
</script>