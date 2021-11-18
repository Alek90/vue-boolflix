<template>
  <div id="app">
    
    <div class="search">

      <input @keyup="createAPI(titleRequired)" v-model="titleRequired" type="text" placeholder="Titolo">

      <button @click="callAPI()">
        Cerca
      </button>

    </div>

    <main id="site_main">

      <div class="container">

        <h2>FILM</h2>

        <div v-for="result in resultsFoundMovies" :key="result.id" class="film">

          <h2>{{result.title}}</h2>

          <p>{{result.original_title}}</p>

          <p>{{result.original_language}}</p>

          <p>{{result.vote_average}}</p>

        </div>


        <h2>TELEFILM</h2>

        <div v-for="result in resultsFoundTvShow" :key="result.id" class="tvshow">

          <h2>{{result.name}}</h2>

          <p>{{result.original_name}}</p>

          <p>{{result.original_language}}</p>

          <p>{{result.vote_average}}</p>

        </div>

      </div>

    </main>

  </div>
</template>

<script>
import axios from 'axios'


export default {
  name: 'App',
  components: {
  },



  data() {
    return {

      titleRequired: '',

      baseApiMovies: ['https://api.themoviedb.org/3/search/movie?api_key=3d29c9625fadd02d13b86c0f4b58f8b7&language=it-IT&page=1&include_adult=false&query='],

      apiRequiredMovies: '',

      resultsFoundMovies: '',

      baseApiTvShow: 'https://api.themoviedb.org/3/search/tv?api_key=3d29c9625fadd02d13b86c0f4b58f8b7&language=it-IT&page=1&include_adult=false&query=',

      apiRequiredTvShow: '',

      resultsFoundTvShow: ''

    }
  },



  methods:{

    /* creazione dell'API in apiRequiredMovies */
    createAPI(required) {
      this.apiRequiredMovies = this.baseApiMovies + required;
      this.apiRequiredTvShow = this.baseApiTvShow + required;
      /* console.log(this.apiRequiredMovies); */
      /* console.log(this.apiRequiredTvShow); */
    },

    /* chiamata dell'API */
    callAPI () {
      axios
      .get(this.apiRequiredMovies)
      .then((response) => {
        console.log((response.data.results));
        this.resultsFoundMovies = response.data.results
      });
      axios
      .get(this.apiRequiredTvShow)
      .then((response) => {
        console.log(response.data.results);
        this.resultsFoundTvShow = response.data.results
      });

    },

  }
}
</script>

<style lang="scss">

</style>
