<template lang="html">
  <div class="data">
    <div class="header">
      <h1>Brewdog Beer App</h1>
    </div>
    <div class="page-container">
      <div class="beer-list">
        <sub>Choose a beer to find out more about it</sub>
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
      if (!this.favouriteBeers.includes(beer)){
        this.favouriteBeers.push(beer);
      } else {
        alert('You have already favourited this beer!');
      }
    })

    eventBus.$on('remove-favourite-beer', (beer) => {
      let position = this.favouriteBeers.indexOf(beer);
      let del = confirm('Are you sure you want to remove this?')
      if (del) {
        this.favouriteBeers.splice(position, 1);
        alert('Item Removed!')
      } else {
        alert('Not Removed!')
      };
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
body {
  background-color: azure;
}

.page-container {
  font-family: helvetica;
}
.header {
  text-align: center;
  background-color: darkslategrey;
  padding: 0.75rem;
  width: 100vmax;
  margin-left: -0.5rem;
  margin-top: -0.5rem;
  color: aliceblue;
}

.beer-list {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 1rem;
}
</style>
