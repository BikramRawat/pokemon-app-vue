<template>
  <div class="detail">
    <div class="detail-view" v-if="show">
      <div v-if="pokemon" class="image">
        <!-- <img v-lazy-load :src="imageUrl + pokemon.id + '.png'" alt="" /> -->
        <img :src="imageUrl + pokemon.id + '.png'" alt="" />
      </div>
      <div v-if="pokemon" class="data">
        <h2>{{ pokemon.name }}</h2>
        <div class="ability">
          <h4>Abilities:</h4>
          <div
            v-for="(value, index) in pokemon.abilities"
            :key="'value' + index"
          >
            {{ value.ability.name }}
          </div>
        </div>
      </div>
      <h2 v-else>OOOOPS ! The pokemon you are searching was not found, search another 👍</h2>
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
    closeDetail() {
      this.$emit("closeDetail");
    },
  },
  created() {
    this.fetchData();
  },
};
</script>
