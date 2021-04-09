<template>

   <v-row justify="center" align="center">
        <v-col cols="12">
            <v-card flat>
              <h1 style="text-align:center;">lista  de usuarios</h1>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn rounded color="rgb(30, 181,181, 0.9)" class="text-none; " @click="registrarUsuario()">Registrar usuario</v-btn>
              </v-card-actions>
        
              <v-data-table
                :headers="headers"
                :items="usuario"
                :items-per-page="5"
                class="elevation-1"
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

    layout:"lHome",
    
      beforeMount(){
          this.getUsuario();
      },
    data () {
      return {
        headers: [
          {
            text: 'id',
            align: 'start',
            value: 'id',
          },
          { text: 'Nombre', value: 'nombre'},
          { text: 'Apellido', value: 'apellido'},
          { text: 'Telefono', value: 'telefono'},
          { text: 'Apartamento', value: 'apartamento' },
          { text: 'Email', value: 'email' },
          { text: 'Clave', value: 'clave' },
          { text: 'Acción', value: 'actions' }
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
        
      },
      
      editItem(item)
      {
        let url= "usuario/" + item.id;
        this.$router.push(url)
      },
      deleteItem(item)
  {
   this.$swal.fire({
  type:"warning",
  title: 'seguro?',
  text: "vas a borrar un registro!",
  icon: 'warning',
  allowEscapeKey:false,
  allowOutsideClick:false,
  showCancelButton:true,
}).then(async(result) => {
  if (result.value) {
    try{
      let url='http://localhost:3001/usuario/' + item.id;
      let response= await this.$axios.delete(url);
      this.$swal.fire({
        type:"success",
        title:"operacion exitosa.",
        text:"el item se elimino correctamente"
      });
      this.getUsuario();
    
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
  registrarUsuario(){
    let url= '/usuario/formulario';
        this.$router.push(url)
  }

  }
  }
</script>