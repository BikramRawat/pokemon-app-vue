<template>
  <div class="home">
    <HelloWorld msg="Welcome to Pokemon App"/>
    <Pokemon />
  </div>
</template>

<script>
import HelloWorld from '@/components/HelloWorld.vue'
import Pokemon from '@/components/Pokemon.vue'

export default {
  name: 'HomeView',
  components: {
    HelloWorld,
    Pokemon
  }
}
</script>
