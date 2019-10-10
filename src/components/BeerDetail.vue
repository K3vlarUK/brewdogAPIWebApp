<template lang="html">
  <div v-if="beer">
    <div class="beer-info">
      <h3>{{ beer.name }}</h3>
      <p>"{{ beer.tagline }}"</p>
      <p><b>Description: </b></p>
      <p>{{ beer.description }}</p>
      <p><b>First Brewed: </b></p>
      <p>{{ beer.first_brewed }}</p>
      <p><b>ABV: </b></p>
      <p>{{ beer.abv }}%</p>
    </div>
    <div class="ingredient-panel">
      <h3 id="ingredient-title">Ingredients</h3>
      <div class="ingredients">
        <div>
          <h4>Malts</h4>
          <li v-for="malt in beer.ingredients.malt">
            {{ malt.name }}
          </li>
        </div>
        <div>
          <h4>Hops</h4>
          <li v-for="hop in uniqueHops">
            {{ hop }}
          </li>
        </div>
        <div>
          <h4>Yeast</h4>
          <li>
            {{ beer.ingredients.yeast }}
          </li>
        </div>
      </div>
    </div>
    <br>
    <div class="add-btn">
      <button id="add-btn" type="button" name="button" @click="addBeerToFav" v-model="beer">Add to Favourites</button>
    </div>
  </div>
</template>

<script>
import {eventBus} from '../main.js';

export default {
  name: 'beer-detail',
  computed: {
    uniqueHops() {
      return this.beer.ingredients.hops.map((hop) => {
        return hop.name
      }).filter((name, index, self) => self.indexOf(name) === index);
    }
  },
  props: ['beer'],
  methods: {
    addBeerToFav() {
      eventBus.$emit('add-favourite-beer', this.beer)
    }
  }
}
</script>

<style lang="css" scoped>
.beer-info {
  display: flex;
  flex-direction: column;
  align-items: center;
  border: 2px solid black;
  padding: 1rem;
}

.ingredient-panel {
  border: 2px solid black;
  padding: 1rem;
}

.ingredients {
  display: flex;
  flex-direction: space-between;
}

.ingredients div {
  border: 2px solid black;
  padding: 1rem;
  flex: 33%;
}

.ingredients li {
  list-style: none;
  text-align: center;
}

.ingredients h4 {
  text-align: center;
  margin-top: -0.8rem;
}

#ingredient-title {
  text-align: center;
  margin-top: -0.5rem;
}

.add-btn {
  display: flex;
  justify-content: center;
}

#add-btn {
  color: black;
  background-color: aliceblue;
}

</style>
