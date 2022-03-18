<template>
  <div id="app">

    <header>
      <input type="text" v-model="search" @keyup.enter="fetchData">
    </header>

    <div v-for="movie in movies" :key="movie.id">
      {{ movie.title }}
    </div>

    <!-- <img alt="Vue logo" src="./assets/download.png">

    <div>
      <input type="text" v-model="search">
      <button>Cerca</button>
    </div>

    <div v-for="movie in movies" :key="movie.id">
      {{ movie.title }}
    </div> -->
    
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'App',
  data() {
    return {
      search: 'batman',
      movies: [],
      baseURL: 'https://api.themoviedb.org/3'
    }
  },

  methods: {
    fetchData: function() {

      axios.get(`${ this.baseURL }/search/movie`, {
        params: {
          api_key: '3c426907b15cb93c3c4d0a11f370a038',
          query: this.search,
          language: 'it-IT'
        }
      }) 
      .then( res => {
        console.log( res.data )
        this.movies = res.data.results
      })
      .catch( error => {
      console.log( error.response )
      })

    }
  },

  // created() {

    // axios.get(`https://api.themoviedb.org/3/search/movie?api_key=3c426907b15cb93c3c4d0a11f370a038&query=${ this.search }`)

    // FILM
    // axios.get(`${ this.baseURL }/search/movie`, {
    //   params: {
    //     api_key: '3c426907b15cb93c3c4d0a11f370a038',
    //     query: this.search,
    //     language: 'it-IT'
    //   }
    // }) 
    // .then( res => {
    //   console.log( res.data )
    //   this.movies = res.data.results
    // })
    // .catch( error => {
    // console.log( error.response )
    // })

  // SERIE TV
    // axios.get(`${ this.baseURL }/search/tv`, {
    //   params: {
    //     api_key: '3c426907b15cb93c3c4d0a11f370a038',
    //     query: this.search,
    //     language: 'it-IT'
    //   }
    // })

  // }
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
