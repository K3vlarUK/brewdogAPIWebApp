<template lang="html">
<div class="data">
  <div class="header">
    <h1>Brewdog Beer App</h1>
  </div>
  <div class="page-container">
    <beer-selecter :beers="beers"></beer-selecter>
  </div>
</div>
</template>

<script>
import {eventBus} from './main.js';
import BeerSelect from './components/BeerSelect.vue';

export default {
  name: 'app',
  data() {
    return {
      beers: [],
      selectedBeer: null
    };
  },
  mounted() {
    fetch('https://api.punkapi.com/v2/beers')
    .then(result => result.json())
    .then(beers => this.beers = beers)

    eventBus.$on('beer-selected', (beer) => {
      this.selectedBeer = beer;
    })
  },
  components: {
    "beer-selecter": BeerSelect
  }
}
</script>

<style lang="css" scoped>
</style>
