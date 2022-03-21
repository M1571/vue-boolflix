// -----------------------------------------
// HTML

<template>

  <div id="app">

    <header class="header">
      <h1>BOOLFIX</h1>
      <input class="in-search" type="text" v-model="search" @keyup.enter="fetchData">
    </header>

    <!-- ------------------------------- -->
    <!-- INIZIO CARD -->

  <main class="main">

    <!-- ------------------------------- -->
    <!-- MOVIE GRID -->

    <h2 class="films">FILM</h2>

    <div class="container grid movie-grid">

      <div v-for="movie in movies" :key="movie.id">

        <img v-if="movie.poster_path" :src="`http://image.tmdb.org/t/p/w342${ movie.poster_path }`" alt="">
        <img v-else src="https://image.tmdb.org/t/p/w342/wwemzKWzjKYJFfCeiB57q3r4Bcm.png" alt="">

        <h3>
        {{ movie.title }}
        </h3>
        <p>
          {{ movie.original_title }}
          <img v-if="flags[ movie.original_language ]" height="11" width="20" :src="flags[ movie.original_language ]"/>
          <span v-else>{{ movie.original_language }}</span>
        </p>
        <span v-for="n in 5" :key="n">
          <i class="fa-star"
            :class=" n <= movie.vote_average ? 'fa-solid gold' : 'fa-regular gray' "
          ></i>
          <!-- [{{ movie.vote_average }}] {{ vote }}  -->
        </span>

      </div>

    </div>

    <!-- FINE MOVIE -->
    <!-- ------------------------------- -->
    <!-- SERIES GRID -->

    <h2>SERIE TV</h2>

    <div class="container grid series-grid">

      <div v-for="serie in series" :key="serie.id">

        <img v-if="tv.poster_path" :src="`http://image.tmdb.org/t/p/w342${ tv.poster_path }`" alt="">
        <img v-else src="https://image.tmdb.org/t/p/w342/wwemzKWzjKYJFfCeiB57q3r4Bcm.png" alt="">

        <h3>
        {{ tv.name }}
        </h3>
        <p>
          {{ serie.original_name }}
          <img v-if="flags[ tv.original_language ]" height="11" width="20" :src="flags[ tv.original_language ]"/>
          <span v-else>{{ tv.original_language }}</span>
        </p>
        <p>
          Voto: [{{ tv.vote_average }}] 
        </p>

      </div>

    </div>

    <!-- FINE SERIES -->
    <!-- ------------------------------- -->

  </main>

    <!-- FINE CARD -->
    <!-- ------------------------------- -->

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

// -----------------------------------------
// JS

<script>
import axios from 'axios'

export default {
  name: 'App',
  data() {
    return {
      search: '',
      movies: [],
      series: [],
      baseURL: 'https://api.themoviedb.org/3',
      flags: {
        en: require('./assets/img/eng.png'),
        it: require('./assets/img/ita.png'),
        fr: require('./assets/img/fra.png'),
        de: require('./assets/img/ger.png'),
        es: require('./assets/img/spa.png'),
        ja: require('./assets/img/jam.jpg'),
        sh: require('./assets/img/sha.png'),
        hi: require('./assets/img/hil.png')
      }
    }
  },

  computed: {
    vote: function() {
      return Math.ceil( this.movies.vote_average / 2)
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

// -----------------------------------------
// CSS

<style lang="scss">

@import './assets/scss/app.scss';
@import '~@fortawesome/fontawesome-free/css/all.css';

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  // text-align: center;
}

.header {
  // margin-top: 50px;
  background-color: #000;
  padding: 30px;
  display: flex;
  justify-content: space-between;
  gap: 30px;
  align-content: center;
  flex-direction: row;
  // border-bottom-right-radius: 15px;
  // border-bottom-left-radius: 15px;
  // border-radius: 15px;
}

h1 {
  color: red;
  align-self: flex-start;
}

.in-search {
  max-height: 30px;
  border-radius: 8px;
}

.films {
  margin-top: 30px;
}

h2 {
  padding: 20px;
  color: darkred;
}

.main {
  min-height: 100vh;
  // background-color: #3C3C3C;
  margin: 20px;
  text-align: center;
}

.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
} 

.gold {
  color: gold;
}

.gray {
  color: darkgray;
}

</style>

// -----------------------------------------
