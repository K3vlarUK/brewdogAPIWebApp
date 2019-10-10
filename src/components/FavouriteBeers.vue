<template lang="html">
  <div class="container">
    <h2>Your Favourite Beers</h2>
    <sub>Click a beer to remove it from your favourites</sub>
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
  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    border: 2px solid black;
    margin-top: 1rem;
  }

  .container li {
    text-align: center;
    list-style: none;
    margin-left: -1.5rem;
  }
</style>
