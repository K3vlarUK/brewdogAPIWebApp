<template lang="html">
  <div class="data">
    <div class="header">
      <h1>Brewdog Beer App</h1>
      <h4>Choose a beer to find out more about it</h4>
    </div>
    <div class="page-container">
      <div class="beer-list">
        <beer-selecter :beers="beers"></beer-selecter>
      </div>
      <br>
      <div class="beer-details">
        <beer-detail :beer="selectedBeer"></beer-detail>
      </div>
      <div class="favourite-beers-list">
        <favourite-beers :beers="favouriteBeers"></favourite-beers>
      </div>
    </div>
  </div>
</template>

<script>
import {eventBus} from './main.js';
import BeerSelect from './components/BeerSelect.vue';
import BeerDetail from './components/BeerDetail.vue';
import FavouriteBeers from './components/FavouriteBeers.vue';

export default {
  name: 'app',
  data() {
    return {
      beers: [],
      selectedBeer: null,
      favouriteBeers: []
    };
  },
  mounted() {
    fetch('https://api.punkapi.com/v2/beers')
    .then(result => result.json())
    .then(beers => this.beers = beers)

    eventBus.$on('beer-selected', (beer) => {
      this.selectedBeer = beer;
    })

    eventBus.$on('add-favourite-beer', (beer) => {
      this.favouriteBeers.push(beer);
    })

    eventBus.$on('remove-favourite-beer', (beer) => {
      let position = this.favouriteBeers.indexOf(beer);
      this.favouriteBeers.splice(position, 1);
    })
  },
  components: {
    "beer-selecter": BeerSelect,
    "beer-detail": BeerDetail,
    "favourite-beers": FavouriteBeers
  }
}
</script>

<style lang="css" scoped>
</style>
