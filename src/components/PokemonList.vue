<template>
  <div class="list">
    <article
      @click="$emit('showDetail', pokemon, allPokeArray)"
      v-for="(pokemon, index) in allPokeArray"
      :key="index"
    >
      <img :src="pokemon.image" alt="" />
      <h3>{{ pokemon.name }}</h3>
    </article>
  </div>
</template>

<!-- eslint-disable no-unused-vars -->
<script setup>
import { defineProps, ref, onMounted, toRefs, watch } from "vue";
import fetchURL from "../config/config.json";
const axios = require("axios");

const props = defineProps({
  setPokemonSearch: String,
});
const { setPokemonSearch } = toRefs(props);

watch(setPokemonSearch, (new_value) => {
  console.log(setPokemonSearch.value);
});



// Fetch API
const infos = ref([]);
onMounted(async () => {
  await axios.get(`${fetchURL.API_URL}` + "/pokemon").then((response) => {
    infos.value = response.data.results;
    makeAllPokeArray();
  });
});

// PokemonList Generation
let allPokeArray = ref([]);

class Pokemon {
  constructor(name, url, image) {
    (this.name = name), (this.url = url), (this.image = image);
  }
}

const makeAllPokeArray = () => {
  for (const pokemon of infos.value) {
    const new_pokemon = new Pokemon(
      pokemon.name,
      pokemon.url,
      `${fetchURL.IMG_URL}${pokemon.name}.png`
    );
    allPokeArray.value.push(new_pokemon);
  }
};
</script>

<style lang="scss" scoped>
.list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  grid-gap: 10px;
  width: 100%;
  max-width: 510px;
}

article {
  height: 150px;
  background-color: #efefef;
  text-align: center;
  text-transform: capitalize;
  border-radius: 5px;
  cursor: pointer;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}

h3 {
  margin: 0;
}

#scroll-trigger {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 150px;
  font-size: 2rem;
  color: #efefef;
}

img {
  width: 96px;
  height: 96px;
}
</style>
