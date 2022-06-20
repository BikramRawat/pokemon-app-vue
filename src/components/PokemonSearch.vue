<template>
  <div class="search-container">
    <div>
      <form @submit.prevent="setPokemonUrl">
        <input
          type="search"
          v-model="input"
          placeholder="Search pokemons ..."
        />
      </form>
    </div>
    <div>
      <button @click="setPokemonUrl">Search</button>
    </div>
  </div>
</template>

<script>
// import pokemonList from "@/components/PokemonList";

export default {
  props: ["apiUrl"],
  data: () => {
    return {
      input: "",
    };
    pokemonList = [];
  },

  methods: {
    setPokemonUrl(url) {
      if (this.input !== "")
        this.$emit("setPokemonUrl", this.apiUrl + this.input.toLowerCase());
    },
    //   computed: {
    //   filteredList() {
    //     return this.pokemonList.filter(pokemon => {
    //       return pokemon.title.toLowerCase().includes(this.search.toLowerCase())
    //     })
    //   }
    // },
  },
};
</script>
