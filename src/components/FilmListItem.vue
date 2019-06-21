<template lang="html">
  <div class="">
    <h2>{{film.title}} | Society score {{film.rt_score}}</h2>
    <button v-if="!inFavourites" v-on:click="handleButton" type="button" name="button">Add Favourite</button>
  </div>
</template>

<script>
import {eventBus} from '@/main.js'

export default {
  name: 'film-list-item',
  props: ['film', 'favourites'],
  computed: {
    inFavourites: function(){
      return this.favourites.includes(this.film)
    }
  },
  methods: {
    handleButton: function(){
      eventBus.$emit('film-selected', this.film)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
