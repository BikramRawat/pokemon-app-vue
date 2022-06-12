<template>
  <div class="searchBar">
    <form @submit.prevent="setPokemonUrl">
      <input type="search" v-model="searchValue" />
    </form>
    <button @click="setPokemonUrl">Search</button>
  </div>
</template>

<script>
export default {
  props: ["apiUrl"],
  data: () => {
    return {
      searchValue: "",
    };
  },

  methods: {
    setPokemonUrl(url) {
      if (this.searchValue !== "")
        this.$emit("setPokemonUrl", this.apiUrl + this.searchValue);
    },
  },
};
</script>
