<template>
<div style="margin-top: 10rem; margin-left:30%"> 
  <v-container>
      <v-card
        outlined
        tile
        width="450"
        height="300"
        color="rgb(77,152,189, 0.1)"
      >
      <h3 style="text-align: center; color:blue">Ingrese a otra dimension </h3>
         <v-form
          ref="form"
          v-model="valid"
          lazy-validation
          class="mt-5"
    
  >
  <div style="margin-top:6rem">
    <v-text-field
      v-model="email"
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
      v-model="clave"
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
      @click="login()"
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


export default {
  components: {
    
  },
  data: () => ({
      valid: true,
      usuario:{
        email:"",
        clave:""
      },
      regla:{
          clave:[ v => !!v || ' Is required'],
          email:[v => /.+@.+\..+/.test(v) || 'E-mail  be valid'],
      },
      }),

    methods: {
      login () {
        this.$router.push("home")
      },
      
    },
}
</script>
