<template>
  <div class="mt-10 p-4 flex flex-wrap">
    <div
      class="ml-4 text-2xl text-blue-400"
      v-for="(pokemon, idx) in pokemons"
      :key="idx"
    >
      <router-link :to="`/about/${idx + 1}`">
        {{ pokemon.name }}
      </router-link>
    </div>
  </div>
</template>

<script>
import { reactive, toRefs } from "vue";
export default {
  setup() {
    const pokemonList = reactive({
      pokemons: []
    });
    fetch("https://pokeapi.co/api/v2/pokemon?offset=0")
      .then((res) => res.json())
      .then((data) => {
        console.log(data);
        pokemonList.pokemons = data.results;
      });

    return { ...toRefs(pokemonList) };
  }
};
</script>
