<template>
  <div id="app">
    
    <HeaderSite :titleRequired="searchTitle" @search="callApi" />
    <MainSite :apiRequiredMovies="apiMovie"  :apiRequiredTvShow="seriesMovie"  :foundMovies="resultsFoundMovies"  :foundTvShow="resultsFoundTvShow" />

  </div>
</template>

<script>
import axios from 'axios';

import HeaderSite from './components/HeaderSite.vue'
import MainSite from './components/MainSite.vue'


export default {
  name: 'App',

  components: {

    HeaderSite,
    MainSite

  },

  data() {
    return {

      searchTitle: '',

      baseApiMovies: 'https://api.themoviedb.org/3/search/movie?api_key=3d29c9625fadd02d13b86c0f4b58f8b7&language=it-IT&page=1&include_adult=false&query=',

      baseApiTvShow: 'https://api.themoviedb.org/3/search/tv?api_key=3d29c9625fadd02d13b86c0f4b58f8b7&language=it-IT&page=1&include_adult=false&query=',

      apiMovie: this.baseApiMovies + this.searchTitle,

      seriesMovie: this.baseApiTvShow + this.searchTitle,

      resultsFoundMovies: '',
    
      resultsFoundTvShow: '',
    }
  },

  methods: {

    /* createAPI(required) {
      this.apiMovie = this.baseApiMovies + required;
      this.seriesMovie = this.baseApiTvShow + required;
      // console.log(this.apiRequiredMovies); 
      // console.log(this.apiRequiredTvShow);
    }, */

    /* chiamata dell'API */
    callApi () {
      axios
      .get(this.apiMovie)
      .then((response) => {
        console.log((response.data.results));
        this.resultsFoundMovies = response.data.results
      });
      axios
      .get(this.seriesMovie)
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
