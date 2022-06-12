<template>
  <div class="detail">
    <div class="detail-view" v-if="show">
      <div v-if="pokemon" class="image">
        <img :src="imageUrl + pokemon.id + '.png'" alt="" />
      </div>
      <div v-if="pokemon" class="data">
        <h2>{{ pokemon.name }}</h2>
        <h3>Abilities</h3>
        <div
          class="ability"
          v-for="(value, index) in pokemon.abilities"
          :key="'value' + index"
        >
          {{ value.ability.name }}
        </div>
      </div>
      <h2 v-else>The pokemon was not found</h2>
      <button class="close" @click="closeDetail">close</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["pokemonUrl", "imageUrl"],
  data: () => {
    return {
      show: false,
      pokemon: {},
    };
  },
  methods: {
    fetchData() {
      let request = new Request(this.pokemonUrl);
      fetch(request)
        .then((response) => {
          if (response.status === 200) return response.json();
        })
        .then((data) => {
          this.pokemon = data;
          this.show = true;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  closeDetail() {
    this.$emit("closeDetail");
  },
  created() {
    this.fetchData();
  },
};
</script>
