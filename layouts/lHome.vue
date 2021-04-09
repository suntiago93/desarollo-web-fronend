<template>
  <app>
      <v-navigation-drawer v-model="openMenu"  app>
      
      <v-list>
          <v-list-item
          v-for="item in items"
          :key="item.id"
          :to="item.to"
          router
          exact>
          <v-list-item-action>
              <v-icon>{{item.icon}}</v-icon>

          </v-list-item-action>
          <v-list-item-content>
              <v-list-item-title v-text="item.title"/>
          </v-list-item-content>
          </v-list-item>
      </v-list>
      </v-navigation-drawer>
      <v-app-bar :clipped-left="clipped" fixed app>
          <v-app-bar-nav-icon @click.stop="openMenu = !openMenu"/>
          <v-toolbar-title v-text="title"/>
      </v-app-bar>
               

      <v-main>
          <v-container fill-height>
              <nuxt/>  
          </v-container>
      </v-main>


       <v-footer app>
           <center >
<v-row>
    <v-col>
        <h3><strong>acerca de </strong> </h3>
        <v-btn  class="text-none" color="white"   plain to="#servicios"><small> Politica de privacidad</small> </v-btn>
        <br>
       <v-btn  class="text-none" color="blue"  plain to="#contacto"> <small> Condiciones de uso</small> </v-btn>
       <br>
       <v-btn  class="text-none" color="blue"  plain to="#contacto"> <small> Creditos</small> </v-btn>
    </v-col>
    <v-col>
        <h3><strong>opiniones </strong></h3>
        <v-btn  class="text-none" color="red"   plain to="#servicios"><small> Lo que dicen nuestros clientes</small> </v-btn>
    </v-col>
</v-row>
<br>
        <span> &copy; {{ new Date().getFullYear() }} TuHábitat Inc. Todos los derechos reservados</span>
           </center>
    </v-footer>
  </app>
</template>

<script>
export default {
data(){
    return{
        openMenu:false,
        clipped:false,
        items:[
             {
            id:"inicio",
            icon:"mdi-home",
            title:"Inicio",
            to:"/home"
            },
            {
            id:"usuario",
            icon:"mdi-account",
            title:" Usuarios",
            to:"/usuario/"
            },
             {
                 id:"instalacion",
            icon:"mdi-home-city",
            title:"  Instalacion",
            to:""
            },
        ],
        
        title:"Administracion"
    };
}
};
</script>

<style>

</style>