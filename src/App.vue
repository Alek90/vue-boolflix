<template>
  <div id="app">
    
    <div class="search">

      <input type="text" placeholder="Titolo">

      <button @click="callAPI">
        Cerca
      </button>

    </div>

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

      titleRequired: 'jurassic',

      apiRequired: 'https://api.themoviedb.org/3/search/movie?api_key=3d29c9625fadd02d13b86c0f4b58f8b7&language=en-US&page=1&query=jurassic&include_adult=false'

      /* la query all'interno del'API deve essere inserita tramite dollegamento con il v-model dell'input, così da determinare la richiesta completa di volta in volta. 
      Punto di partenza:
        -Come inserisco la stringa del v-model nella query?
       */

    }
  },

  methods:{

    callAPI () {
      axios.get(this.apiRequired)
      .then((response) => {
        console.log((response.data.results));
      })
    }
  }
}
</script>

<style lang="scss">

</style>
