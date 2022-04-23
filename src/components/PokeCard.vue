<template>
  <v-card
    :loading="loading"
    class="mx-8 my-12 hola"
    width="250"
    id="PokeItem"
    v-if="datosPoke"
  >
    <v-img
      height="250"
      :src="datosPoke.sprites.front_default"
      class="image"
      :style="{ backgroundColor: cambiarColor(datosPoke.types[0].type.name) }"
    ></v-img>

    <v-card-title>{{ dato.name.toUpperCase() }}</v-card-title>
    <v-chip
      :style="{ backgroundColor: cambiarColor(datosPoke.types[0].type.name) }"
      class="mb-6"
    >
      {{ datosPoke.type.toUpperCase() }}
    </v-chip>
    <br />
    <br />
    <v-dialog transition="dialog-bottom-transition" max-width="600">
      <template v-slot:activator="{ on, attrs }">
        <v-btn color="black" v-bind="attrs" v-on="on">From the bottom</v-btn>
      </template>
      <template v-slot:default="dialog">
        <v-card>
          <v-toolbar color="primary" dark>Opening from the bottom</v-toolbar>
          <v-card-text>
            <div class="text-h2 pa-12">Hello world!</div>
          </v-card-text>
          <v-card-actions class="justify-end">
            <v-btn text @click="dialog.value = false">Close</v-btn>
          </v-card-actions>
        </v-card>
      </template>
    </v-dialog>
  </v-card>
</template>

<script>
import axios from "axios";

export default {
  name: "PokeCard",
  props: {
    dato: Object,
    index: Number,
  },
  data: () => ({
    datosPoke: {
      type: [],
      weight: Number,
      height: Number,
      id: Number,
      base_experience: Number,
    },
    loading: false,
    selection: 1,
    dialog: false,
  }),

  methods: {
    cambiarColor(type) {
      switch (type) {
        case "grass":
          return "#34eb86";
        case "fire":
          return "#eb3453";
        case "water":
          return "#3474eb";
        case "bug":
          return "#b2bd55";
        case "poison":
          return "#a502b8";
        case "ground":
          return "#4d4d4d";
        case "electric":
          return "#f2ff00";
        case "fairy":
          return "#9c9100";
        case "normal":
          return "#1d232e";
        case "fighting":
          return "#f06e1d";
      }
    },
  },
  mounted() {
    axios.get(this.dato.url).then((response) => {
      this.datosPoke = response.data;
      this.datosPoke.type = response.data.types[0].type.name;
      this.datosPoke.weight = response.data.weight;
      this.datosPoke.height = response.data.height;
      this.datosPoke.id = response.data.id;
      this.datosPoke.base_experience = response.data.base_experience;
      //console.log(response);
    });
  },
};
</script>
<style scoped>
.hola {
  margin-left: 30px !important;
  margin-right: 30px !important;
}
</style>
