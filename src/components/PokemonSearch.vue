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
export default {
  props: ["apiUrl"],
  data: () => {
    return {
      input: "",
    };
  },

  methods: {
    setPokemonUrl(url) {
      if (this.input !== "")
        this.$emit("setPokemonUrl", this.apiUrl + this.input.toLowerCase());
    },
  },
};
</script>
