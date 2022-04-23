<template>
  <div id="Index">
    <img src="../assets/pokee.png" alt="" />
    <div class="cards">
      <div v-for="(item, index) in data" v-bind:key="index">
        <PokeCard :dato="item" :index="index" cols="3" md="2" />
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import PokeCard from "../components/PokeCard";

export default {
  name: "Index",
  components: {
    PokeCard,
  },
  data() {
    return {
      data: [],
    };
  },
  mounted() {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=60").then((response) => {
      this.data = response.data.results;
      //console.log(this.data);
    });
  },
};
</script>
<style>
.cards {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
</style>