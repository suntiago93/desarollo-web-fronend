<template>
<div style="margin-top: 10rem; margin-left:30%"> 
  <v-container >
      <v-card
        outlined
        tile
        width="450"
        height="300"
        color="rgb(77,152,189, 0.1)"
      >
      <h3 style=" color:blue">Ingrese a otra dimension </h3>
         <v-form
          ref="formularioLogin"
          v-model="valid"
          lazy-validation
          class="mt-5"
    
  >
  <div style="margin-top:6rem">
    <v-text-field
      v-model="usuario.email"
      :rules="regla.email"
      label="Email"
      required
      outlined
      filled
      rounded
      dense
      
    ></v-text-field>
</div>
    <v-text-field
      v-model="usuario.clave"
      :rules="regla.clave"
      label="clave"
      type="password"
      required
      outlined
      filled
      rounded
      dense
    ></v-text-field>
    <div style="margin-left:25%">
    <v-btn
      :disabled="!valid"
      color="rgb(30, 181,181, 0.3)"
      width="200px"
      @click="login"
      rounded
      
    >
    <span> Ingresar </span>
    </v-btn>
    </div>
         </v-form>
      </v-card>
  </v-container>
    </div>
</template>

<script>
const url_api='http://localhost:3001/usuario/';

export default {
  data: () => ({
      valid: true,
     usuario:{
       email:"",
       clave:"",
     },
      regla:{
          clave:[ v => !!v || ' Is required'],
          email:[v => /.+@.+\..+/.test(v) || 'E-mail  be valid'],
      },
      }),

    methods: {
    async login () {
        if (this.$refs.formularioLogin.validate()) {
          let response = await this.$axios.get(url_api);
          let usuarios=response.data;
          let buscar=usuarios.find(x=>{return x.email == this.usuario.email && x.clave == this.usuario.clave});
          if(buscar)
          {
            this.$router.push("/home")
          }
          else{
            this.$swal.fire({
              type:"error",
              title: "opps",
              text:"El correo o o clave son incorrectas",
              allowEscapekey:false,
              allowOutsideClick:false,
            })
          }
        } else {
          this.$swal.fire({
            type:"warning",
            title:"Formulario incompleto.",
            text: "hay campos "
          })
        }
        
      },
      
    },
}
</script>
