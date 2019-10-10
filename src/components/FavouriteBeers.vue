<template lang="html">
  <div>
    <h2>Your Favourite Beers</h2>
    <ul>
      <li v-for="beer in beers" @click="removeFavBeer">
        {{ beer.name }}
      </li>
    </ul>
  </div>
</template>

<script>
import {eventBus} from '../main.js';

export default {
  name: 'favourite-beers',
  props: ['beers'],
  methods: {
    removeFavBeer() {
      eventBus.$emit('remove-favourite-beer', this.beer)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
