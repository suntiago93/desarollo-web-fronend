<template>
  <v-carousel v-model="model">
    <v-carousel-item
      v-for="(item, i) in items"
      :key="i"
      :src="item.src"
    >
     
    </v-carousel-item>
  </v-carousel>
</template>

<script>
  export default {
    name: "Hero",
    data: () => ({
      model: 0,
      items: [
       {
          src: '/images/unidadResidencial.png',
          title: "pagos"
        },
        {
          src: '/images/unidadResidencial.png',
          title: "reservas"
        },
        {
          src: '/images/unidadResidencial.png',
          title: "informacion"
        }
      ],
    }),
  }
</script>