<template>
  <div class="my-8">
    <h2>Testimonios SPL</h2>
    <h2>Edición Especial Mujeres TI</h2>
    <!-- Nombre del Team -->
    <h2>Las Cazadoras</h2>
    <v-row class="row-container mt-9">
      <v-col v-for="testimonio in testimonios" :key="testimonio.id" cols="12" sm="6" md="4" lg="3">
        <v-card shaped class="mb-4">
          <v-card-title class="headline">
            <v-icon class="mr-2">mdi-account</v-icon>
            {{ testimonio.nombre }}
          </v-card-title>
          <v-card-text>
            <v-icon class="mr-2">mdi-text-account</v-icon>
            {{ testimonio.descripcion }}
          </v-card-text>
          <v-card-text>
            <v-icon class="mr-2">mdi-linkedin</v-icon>
            <a :href="testimonio.socialUrl" target="_blank" rel="noopener noreferrer">{{ testimonio.socialUrl }}</a>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  data() {
    return {
      testimonios: [],
    };
  },

  created() {
    this.obtenerTestimonios();
  },

  methods: {
    // Solicitud HTTP GET para obtener los testimonios desde el servidor
    obtenerTestimonios() {
      fetch(`${process.env.VUE_APP_SERVER_URL}api/obtener-testimonios`)
        .then(response => response.json())
        .then(data => {
          this.testimonios = data;
        })
        .catch(error => {
          console.error(error);
        });
    },
  },
};
</script>

<style lang="scss" scoped>
@media only screen and (max-width: 600px) {

  h2 {
    font-size: 25px !important;
    padding: 0 20px !important;
  }

}

h2 {
  text-align: center;
  font-size: 30px;
  font-weight: bold;
  color: #165c66;
}

.headline {
  font-size: 18px;
  font-weight: bold;
}

.v-card {
  height: 250px;
  overflow-y: auto;
  padding: 6px;
}

.row-container {
  width: 95%;
  margin: 0 auto;
}
</style>
