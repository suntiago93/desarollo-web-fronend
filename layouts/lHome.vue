<template>
  <v-app>
      <v-navigation-drawer v-model="openMenu"  app>
      
      <v-list>

          <v-list-item v-for="item in items" :key="item.id" :to="item.to" router exact>
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

      <v-footer
      :absolute="!fixed"
      app
      padless
    >
    <div > &copy; {{ new Date().getFullYear() }} TuHábitat Inc. Todos los derechos reservados</div>
    </v-footer>  
      
  </v-app>
</template>

<script>
export default {
data(){
    return{
        fixed:false,
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
            id:"reservas",
            icon:"mdi-calendar-plus",
            title:"Reservas",
            to:"/reservas/"
            },
             {
            id:"instalacion",
            icon:"mdi-home-city",
            title:"  Instalacion",
            to:"/instalacion/"
            },
            {
            id:"salir",
            icon:"mdi-exit-to-app",
            title:" salir",
            to:"/"
            },
        ],
        
        title:"Administracion"
    };
}
};
</script>

<style>

</style>