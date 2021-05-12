
<template>

  <v-row align="center">
    <v-item-group
      v-model="window"
      class="shrink mr-6"
      mandatory
      tag="v-flex"
    >
      <v-item
        v-for="i in length"
        :key="i"
        v-slot="{ active, toggle }"
      >
        <div>
          <v-btn
            :input-value="active"
            icon
            @click="toggle"
          >
            <v-icon>mdi-record</v-icon>
          </v-btn>
        </div>
      </v-item>
    </v-item-group>

    <v-col>
      <v-window
        v-model="window"
        class="elevation-1"
        vertical
      >
        <v-window-item
          v-for="(slide, i) in slides"
          :key="i"
        
          
        >
          <v-card flat>
            <v-card-text>
              <v-row
                class="mb-4"
                align="center"
              >
                <v-avatar
                  color="grey"
                  class="mr-4"
                ></v-avatar>
                <strong class="title">Mark nissim {{ i }}</strong>
                <v-spacer></v-spacer>
                <v-btn icon>
                  <v-icon>mdi-account</v-icon>
                </v-btn>
                <v-spacer></v-spacer>
       
              </v-row>
                <v-img
                  height="200"
                   src='/images/triangulos.png'
    >
                 </v-img>
                 <v-spacer></v-spacer>
              <h1 style="color:blue">
                <strong class="title"> {{ slide.titulo }}</strong>
              </h1>

              <p>
                {{ slide.parrafo1 }}
              </p>

              <p>
                {{ slide.parrafo2 }}
              </p>
            </v-card-text>
          </v-card>
        </v-window-item>
      </v-window>
    </v-col>
  </v-row>
</template>

<script>
export default {
    layout:"lHomeUser",
    data: () => ({
      length: 3,
      window: 0,
      slides: [
        {
        titulo:  'Tikvá',
        parrafo1: 'La Unidad Tikvá, es una unidad diseñada para su comodidad. Cuenta con varias areas sociales como la piscina, salon de fiesta, sala de estudio y gimnacio.',
        parrafo2: 'Debido a la pandemia mundial se creo la aplicacion web la cual fortalece el bien estar de los recidentes y disminiye el riesgo a contagiarse.'
        },
        {
        titulo:  'Piscina',
        parrafo1: 'La piscina esta abierta de 8:00 - 20:00 hs, la cual podran realizar reservas de una duracion de 4:00 hs. ',
        parrafo2: 'La piscina es apta para mayores de 3 años, se pide el favor de dejar el establecimeinto como se encontro al llegar.'
        },
        {
        titulo:  'Gimnacio',
        parrafo1: 'SECOND Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.',
        parrafo2: 'THI Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.',
        }
        ],
        
    }),
}
</script>



