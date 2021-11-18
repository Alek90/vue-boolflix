<template>
  <div id="app">
    
    <div class="search">

      <input @keyup="createAPI()" v-model="titleRequired" type="text" placeholder="Titolo">

      <button @click="callAPI ()">
        Cerca
      </button>

    </div>

    <main id="site_main">

      <div class="container">

        <div v-for="result in resultsFound" :key="result.id" class="film">

          <h2>{{result.title}}</h2>

          <p>{{result.original_title}}</p>

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

      baseApi: ['https://api.themoviedb.org/3/search/movie?api_key=3d29c9625fadd02d13b86c0f4b58f8b7&language=it&page=1&include_adult=false&query='],

      apiRequired: '',

      resultsFound: ''

      /* la query all'interno del'API deve essere inserita tramite collegamento con il v-model dell'input, così da determinare la richiesta completa di volta in volta. 
      Punto di partenza:
        -Come inserisco la stringa del v-model nella query?
       */

    }
  },



  methods:{

    /* creazione dell'API in apiRequired */
    createAPI() {
      this.apiRequired = this.baseApi + this.titleRequired;
      console.log(this.apiRequired);
    },

    /* chiamata dell'API */
    callAPI () {
      axios.get(this.apiRequired)
      .then((response) => {
        console.log((response.data.results));
        this.resultsFound = response.data.results;
        console.log(this.resultsFound);
      })
    }
  }
}
</script>

<style lang="scss">

</style>
