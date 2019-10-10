<template lang="html">
  <div>
    <select @change="selectBeer" v-model="beer">
      <option v-for="beer in beers" :value="beer">
        {{ beer.name }}
      </option>
    </select>
  </div>
</template>

<script>
import {eventBus} from '../main.js';

export default {
  name: 'beer-selecter',
  data() {
    return {
      beer: null
    }
  },
  props: ['beers'],
  methods: {
    selectBeer() {
      eventBus.$emit('beer-selected', this.beer)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
