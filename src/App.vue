<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">

    <div>
      <input type="text" v-model="search">
    </div>

    <div v-for="movie in movies" :key="movie.id">
      {{ movie.title }}
    </div>
    
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'App',
  data() {
    return {
      search: 'ritorno',
      movies: []
    }
  },
  created() {

    axios.get('https://api.themoviedb.org/3/search/movie?api_key=3c426907b15cb93c3c4d0a11f370a038&query=batman')
    .then( res => {
      console.log( res.data )
      this.movies = res.data.results
    })
    .catch( error => {
    console.log( error.response )
    })

  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
