<template>
  <div class="ServicesAdminComponent">
    <b-container>
      <div>
        <b-button variant="primary" v-on:click="cerrarSesion">Cerrar sesión</b-button>
      </div>
    </b-container>
    <br />
    <b-container>
      <b-row align-v="center">
        <b-col
          class="bv-example-row"
          v-for="service in servicesList"
          :key="service.name"
          md="3"
        >
          <b-card tag="service" style="max-width: 20rem" class="mb-2" footer="Servicio">
            <h1>{{ service.name }}</h1>
            <b-card-text>
              {{ service.inCharge }} <br />
              Range: {{ service.cost }} <br />
              Rate: {{ service.rate }} <br />
            </b-card-text>
            <!-- <b-col md="2"> -->
              <b-button variant="secondary" v-on:click="serviceDelete(service._id)"
                >Eliminar</b-button
              >
            <!-- </b-col> -->
            <!-- <b-button variant="primary" v-on:click="book">Agendar cita</b-button> -->
          </b-card>
        </b-col>
      </b-row>
    </b-container>
    <br />
    <b-container>
      <b-row align-v="center">
        <b-col md="2">
          <b-button variant="primary" v-on:click="serviceAdd">Agregar servicio</b-button>
        </b-col>
        <b-col md="2">
          <b-button variant="secondary" v-on:click="serviceList">Lista de citas</b-button>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "ServicesAdminComponent",
  props: {
    servicesList: null,
  },
  data: function () {
    return {
      form: {
        title: "",
        description: "",
        manager: "",
      },
    };
  },
  methods: {
    cerrarSesion() {
      this.$router.push("/");
    },
    serviceAdd() {
      this.$router.push("ServicesAdd");
    },
    serviceEdit() {
      this.$router.push("ServicesEdit");
    },
    serviceList() {
      this.$router.push("Booked");
    },
    serviceDelete(_id) {
      console.log("Entramos a función eliminar: ", _id);
      axios
        .delete(`http://localhost:3001/servicios/eliminar/${_id}`)
        .then((result) => {
          console.log(result);
          this.$router.push("ServicesAdmin");
        })
        .catch((e) => console.log(e));
    },
  },
};
</script>

<style scoped>
.left {
  text-align: left;
}
</style>
