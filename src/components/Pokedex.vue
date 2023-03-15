<!-- eslint-disable no-unused-vars -->


<script setup>

import { ref } from "vue";

import PokemonDetail from "../components/PokemonDetail.vue";
import PokemonList from "../components/PokemonList.vue";
import PokemonSearch from "../components/PokemonSearch.vue";

// Modal PokemonDetail
const showModal = ref(false);
const pokeDetail = ref(null)

function show(pokemon) {
  pokeDetail.value = pokemon;
  showModal.value = true
  console.log(pokemon)
}

function hide() {
  showModal.value = false
}

</script>

<template>
  <div class="container">
    <PokemonSearch />
    <PokemonDetail @hideDetail="hide" v-if="showModal" :pokemon="pokeDetail" />
    <PokemonList @showDetail="show" />
  </div>
</template>

<style lang="scss" scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 10px;
  width: calc(100% - 20px);
  min-height: calc(100vh - 20px);
  //background: radial-gradient(#ffbf0b, #e20000);

  font-family: "Acme", arial;
  font-size: 1rem;
  font-weight: normal;
}

h1 {
  color: #efefef;
}
</style>