<template>
  <div class="search-container">
    <div>
    <form @submit.prevent="setPokemonUrl">
      <input type="search" v-model="searchValue" />
    </form>
    </div>
    <div>
    <button @click="setPokemonUrl()">Search</button>
    </div>
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
        this.$emit("setPokemonUrl", this.searchValue);
    },
  },
};
</script>
