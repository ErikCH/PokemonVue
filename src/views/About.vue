<template>
  <div class="about">
    <div
      v-if="pokemon"
      className="w-3/12 m-auto bg-purple-100 mt-4 shadow-2xl flex justify-center flex-col items-center"
    >
      <h3 className="text-2xl text-green-900 uppercase">{{ pokemon.name }}</h3>
      <div class="flex justify-center">
        <img className="w-48" :src="pokemon.sprites.front_shiny" alt="" />
        <img className="w-48" :src="pokemon.sprites.back_shiny" alt="" />
      </div>
    </div>
  </div>
</template>

<script>
import { reactive, toRefs } from "vue";
import { useRoute } from "vue-router";

export default {
  setup() {
    const route = useRoute();

    const pokemon = reactive({
      pokemon: ""
    });
    fetch(`https://pokeapi.co/api/v2/pokemon/${route.params.slug}/`)
      .then((res) => res.json())
      .then((data) => {
        pokemon.pokemon = data;
        console.log(data);
      });
    return { ...toRefs(pokemon) };
  }
};
</script>
