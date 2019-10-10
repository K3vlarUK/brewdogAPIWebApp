<template lang="html">
  <div v-if="beer">
    <h3>{{ beer.name }}</h3>
    <p>"{{ beer.tagline }}"</p>
    <p>Description: {{ beer.description }}</p>
    <p>First Brewed: {{ beer.first_brewed }}</p>
    <p>ABV: {{ beer.abv }}%</p>
  </div>
</template>

<script>
export default {
  name: 'beer-detail',
  props: ['beer']
}
</script>

<style lang="css" scoped>
</style>
