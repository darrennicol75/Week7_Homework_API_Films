<template>
  <div id="app">
    <h1>The Howling Wolf Film Society</h1>
    <h2>Top Picks 2019</h2>
    <div id="app2">
      <nav> <router-link :to="{ name: 'film'}">Film</router-link>
      | <router-link :to="{ name: 'favourite'}">Favourite</router-link>
      </nav>
    </div>
    <router-view :films="films" :favourites="favourites" id="view"></router-view>
  </div>

</template>

<script>
import { eventBus } from '@/main.js'
import FilmList from './components/FilmList.vue'

export default {
  name: 'app',
  data(){
    return {
      films: [],
      favourites: []
    }
  },
  mounted(){
    fetch("https://ghibliapi.herokuapp.com/films")
    .then(res => res.json())
    .then(films => this.films = films)

    eventBus.$on('film-selected', (film) => {
      this.favourites.push(film)
    })
  },
  components: {
    "film-list": FilmList
  }
}
</script>

<style>
#app {
  font-family: sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #7CFFC4;
  margin-top: 60px;
  /* background-image: url('./src/assets/mj2.jpg') */
  background-color: #33A1FD;
}
#app2 {
  font-family: sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: black;
  margin-top: 10px;
  /* background-image: url('./src/assets/mj2.jpg') */
  background-color: white;
}
</style>


    <!-- // fetch("http://strainapi.evanbusse.com/dxyTKu0/strains/search/all") -->
        <!-- // fetch("https://api.punkapi.com/v2/beers") -->
