<template>
 


 

  <v-card
    color="rgb(8, 239, 247)"
    
  >
    <v-img
      height="200"
      src='/images/triangulos.png'
    >
    </v-img>
    <v-form>
      <v-container justify="center" align="center"  >
        <v-row>
          <v-col
            cols="12"
            md="6"
          >
            <v-text-field
              filled
              color="blue-grey "
              label="Nombre"
              :disabled="valid"
            ></v-text-field>
          </v-col>
          <v-col
            cols="12"
            md="6"
          >
            <v-text-field
              filled
              color="blue-grey lighten-2"
              label="Apellido"
              :disabled="valid"
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="6">
           <v-text-field
              filled
              color="blue-grey lighten-2"
              label="Telefono"
              :disabled="valid"
            ></v-text-field>
            </v-col>
            <v-col cols="12" md="6">
             <v-text-field
              filled
              color="blue-grey lighten-2"
              label="Apartamento"
              :disabled="valid"
            ></v-text-field>
            </v-col>
            <v-col cols="12" md="6">
             <v-text-field
              filled
              color="blue-grey lighten-2"
              label="Parqueadero"
              :disabled="valid"
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="6">
             <v-text-field
              filled
              color="blue-grey lighten-2"
              label="Clave"
              :disabled="valid"
            ></v-text-field>
          </v-col>
          <v-col cols="12" >
             <v-text-field
              filled
              color="blue-grey lighten-2"
              label="Email"
              :disabled="valid"
            ></v-text-field>
          </v-col>
        </v-row>
      </v-container>
    </v-form>
    <v-divider></v-divider>
  </v-card>
  
 


</template>

<script>

  export default {
      layout:"lHomeUser",
  
  data:()=>({
valid: true
  })
  }
</script>


  <style <style lang="scss">
#a {
    background:rgba(8, 239, 247),
}
</style>

8, 239, 247

