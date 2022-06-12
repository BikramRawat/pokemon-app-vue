<template>
  <div class="pokemon-list">
    <section
      v-for="(pokemon, index) in pokemons"
      :key="'poke' + index"
      @click='setPokemonUrl(pokemon.url)'
    >
      <img
        :src="imageUrl + pokemon.id + '.png'"
        width="90"
        height="90"
        alt="pokemon image"
      />
      <h3>{{ pokemon.name }}</h3>
    </section>
  </div>
</template>

<script>
import PokemonDetails from "@/components/PokemonDetails";
export default {
  props: ["imageUrl", "apiUrl"],

  data: () => {
    return {
      pokemons: [],
      nextUrl: "",
      currentUrl: "",
      imageUrl: "",
      apiUrl: "https://pokeapi.co/api/v2/pokemon",
      pokemanUrl: "",
      showDetail: false,
    };
  },

  components: {
    PokemonDetails,
  },

  methods: {
    fetchData() {
      let request = new Request(this.apiUrl);
      fetch(request)
        .then((response) => {
          if (response.status === 200) return response.json();
        })
        .then((data) => {
          this.nextUrl = data.next;
          data.results.forEach((pokemon) => {
            pokemon.id = pokemon.url
              .split("/")
              .filter(function (part) {
                return !!part;
              })
              .pop();
            this.pokemons.push(pokemon);
          });
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  next() {
    this.currentUrl = this.nextUrl;
    this.fetchData();
  },
  setPokemonUrl(url) {
    this.$emit("setPokemonUrl", url);
  },
  created() {
    this.currentUrl = this.apiUrl;
    this.fetchData();
  },
};
</script>
