<template>
  <v-app>
      <v-navigation-drawer v-model="openMenu" color="rgb(8, 239, 247)" app>
      
      <v-list>

          <v-list-item v-for="item in items" :key="item.id" :to="item.to" router exact>
          <v-list-item-action>
              <v-icon style="color:white">{{item.icon}}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
              <v-list-item-title style="color:grey " v-text="item.title"/>
          </v-list-item-content>
          </v-list-item>
      </v-list>
      
      </v-navigation-drawer>
      <v-app-bar :clipped-left="clipped" color="rgb(8, 239, 247)" fixed app>
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
            to:"/homeUser"
            },
            {
            id:"perfil",
            icon:"mdi-account",
            title:" Perfil",
            to:"/usuario/perfil/"
            },
             {
            id:"reservas",
            icon:"mdi-calendar-plus",
            title:"Reservas",
            to:"/reservasUser/"
            },
             {
            id:"pagos",
            icon:"mdi-currency-usd-circle-outline",
            title:"Pagos",
            to:"/reservasUser/pago/"
            },
            {
            id:"salir",
            icon:"mdi-exit-to-app",
            title:" salir",
            to:"/"
            },
        ],
        
        title:"TuHabitat "
    };
}
};
</script>

<style>

</style>