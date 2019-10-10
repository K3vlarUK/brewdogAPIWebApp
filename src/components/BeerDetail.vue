<template lang="html">
  <div v-if="beer">
    <div class="beer-info">
      <h3>{{ beer.name }}</h3>
      <p>"{{ beer.tagline }}"</p>
      <p>Description: {{ beer.description }}</p>
      <p>First Brewed: {{ beer.first_brewed }}</p>
      <p>ABV: {{ beer.abv }}%</p>
    </div>
    <div class="add-btn">
      <button type="button" name="button" @click="addBeerToFav" v-model="beer">Add to Favourites</button>
    </div>
  </div>
</template>

<script>
import {eventBus} from '../main.js';

export default {
  name: 'beer-detail',
  props: ['beer'],
  methods: {
    addBeerToFav() {
      eventBus.$emit('add-favourite-beer', this.beer)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
