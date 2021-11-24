<template>
  <div id="app">

    <header class="flex" id="site_header">

      <h1>BOOLFLIX</h1>

      <!-- componente di ricerca -->
      <div class="search_form">

        <input @keyup="createApi(titleRequired)" v-model="titleRequired" type="text" placeholder="Title" value="Title">

        <font-awesome-icon @click="callApi()" :icon="['fas', 'search']" class="search_start" />

      </div>

    </header>
    <!-- /header -->



    <main id="site_main">
       
      <!-- contenuto principale del #site_main -->
      <div class="results_found">

        <!-- film trovati -->
        <div class="films_found">  

          <h2>FILM</h2>

          <div class="container flex">

            <div v-for="result in resultsFoundMovies" :key="result.id" class="film col_3">
            
              <div v-if="result.poster_path != null" class="poster">
              
                <img :src="posterUrl + result.poster_path" :alt="result.title"> 

              </div>

              <div v-else class="poster_null">

                <h3>{{result.title}}</h3>

              </div>
              

              <div class="info">

                <h3>{{result.title}}</h3>

                <h4 class="">{{result.original_title}}</h4>

                <span class="language" v-if="viewFlag(result.original_language)">
                
                  <country-flag :country= "result.original_language === 'en' ? 'gb' : result.original_language" size='big'/>

                </span>
                
                <p v-else>{{result.original_language}}</p>

                <div class="vote">

                  <font-awesome-icon class="star" v-for="(vote, index) in Math.ceil(result.vote_average/2)" :key="index" :icon="['fas', 'star']" />
            
                  <font-awesome-icon class="star" v-for="unvote in Math.abs(5 - Math.ceil(result.vote_average/2))" :key="unvote+'x'" :icon="['far', 'star']" />

                </div>

                <p class="overview">{{result.overview}}</p>

              </div>


            </div>

          </div>
              
        </div>

        <!-- serie tv trovate -->
        <div class="tv_found">


          <h2>TV</h2>

          <div class="container flex">

            <div v-for="result in resultsFoundTvShow" :key="result.id" class="tvshow col_3">

              <div v-if="result.poster_path != null" class="poster">

                <img :src="posterUrl + result.poster_path" :alt="result.name">

              </div>
              
              <div v-else class="poster_null">

                <h3>{{result.name}}</h3>

              </div>

              <div class="info">

                <h3>{{result.name}}</h3>

                <h4>{{result.original_name}}</h4>

                <span class="language" v-if="viewFlag(result.original_language)">
                
                  <country-flag :country= "result.original_language === 'en' ? 'gb' : result.original_language" size='big'/>

                </span>
                
                <p v-else>{{result.original_language}}</p>

                <div class="vote">

                  <font-awesome-icon class="star" v-for="(vote, index) in Math.ceil(result.vote_average/2)" :key="index" :icon="['fas', 'star']" />
            
                  <font-awesome-icon class="star" v-for="(unvote, index) in Math.abs(5 - Math.ceil(result.vote_average/2))" :key="index+'x'" :icon="['far', 'star']" />

                </div>

                <p class="overview">{{result.overview}}</p>

              </div>


            </div>

          </div>

        </div>

      </div>

    </main>
    <!-- /main -->
    
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',

  data() {
    return {

      titleRequired: '',

      baseApiMovies: 'https://api.themoviedb.org/3/search/movie?api_key=3d29c9625fadd02d13b86c0f4b58f8b7&language=it-IT&page=1&include_adult=false&query=',

      baseApiTvShow: 'https://api.themoviedb.org/3/search/tv?api_key=3d29c9625fadd02d13b86c0f4b58f8b7&language=it-IT&page=1&include_adult=false&query=',

      apiMovie: '',

      seriesMovie: '',

      resultsFoundMovies: '',
    
      resultsFoundTvShow: '',

      posterUrl: 'https://image.tmdb.org/t/p/w342',

      poster: '',

      flagUrl: 'https://flagcdn.com/16x12/',

      flag: ["it", "fr", "de", "es", "en", "nl", "fi", "no"]
    }
  },



  methods: {
    /* creazione dell'API in apiRequiredMovies */
    createApi(required) {
      this.apiMovie = this.baseApiMovies + required;
      this.seriesMovie = this.baseApiTvShow + required;
      // console.log(this.apiRequiredMovies); 
      // console.log(this.apiRequiredTvShow);
    },

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
      this.titleRequired = '';
      

    },

    viewFlag(isoCode) {
      return this.flag.includes(isoCode)
    },

  },
}
</script>

<style lang="scss">

@import "./assets/scss/style.scss";

</style>
