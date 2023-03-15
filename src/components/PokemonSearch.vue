<template>
  <div class="searchbar">
    <input v-model="userSearchPokemon" type="text" placeholder="PokeSearch" />
  </div>
</template>

<!-- eslint-disable no-unused-vars -->
<script setup>
import { ref, watch, defineProps, defineEmits } from "vue";

const props = defineProps({
  pokeArray: Array,
});

let pokeArray = [];

let userSearchPokemon = ref("");

//let resultSearchPokemon = ref([]);
const emit = defineEmits(["searchPokemonEmit"]);

watch(userSearchPokemon, (new_value) => {
  emit("searchPokemonEmit", new_value);
});
</script>

<style scoped>
.searchbar {
  position: relative;
  width: 100%;
  max-width: 510px;
  padding-bottom: 20px;
}

input {
  border: none;
  outline: none;
  border-radius: 5px;
  padding: 10px 40px 10px 10px;
  width: calc(100% - 50px);
  font-size: 1rem;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}
</style>
