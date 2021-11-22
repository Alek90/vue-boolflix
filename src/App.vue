<template>
  <div id="app">

    <header class="flex" id="site_header">

      <h1>BOOLFLIX</h1>

      <!-- componente di ricerca -->
      <div class="search_form">

        <input @keyup="createApi(titleRequired)" v-model="titleRequired" type="text" placeholder="Titolo">

        <font-awesome-icon @click="callApi()" :icon="['fas', 'search']" class="search_start" />

      </div>

    </header>

    <main id="site_main">
       
      <!-- contenuto principale del #site_main -->
      <div class="results_found">

        <!-- film trovati -->
        <div class="films_found">  

          <h2>FILM</h2>

          <div class="container flex">

            <div v-for="result in resultsFoundMovies" :key="result.id" class="film col_3">
            
              <img :src="posterUrl + result.poster_path" alt=""> 

              <div class="info">

                <h3>{{result.title}}</h3>

                <p>{{result.original_title}}</p>

                <country-flag :country= "result.original_language === 'en' ? 'gb' : result.original_language" size='big'/>

                <div class="vote">

                  <font-awesome-icon class="star" v-for="(vote, index) in Math.ceil(result.vote_average/2)" :key="index" :icon="['fas', 'star']" />
            
                  <font-awesome-icon class="star" v-for="unvote in Math.abs(5 - Math.ceil(result.vote_average/2))" :key="unvote+'x'" :icon="['far', 'star']" />

                </div>

              </div>


            </div>

          </div>
              
        </div>

        <!-- serie tv trovate -->
        <div class="tv_found">


          <h2>TELEFILM</h2>

          <div class="container flex">

            <div v-for="result in resultsFoundTvShow" :key="result.id" class="tvshow col_3">
              
              <img :src="posterUrl + result.poster_path" alt="">

              <h3>{{result.name}}</h3>

              <p>{{result.original_name}}</p>

              <country-flag country='result.original_language' size='big'/>

              <div class="vote">

                <font-awesome-icon v-for="(vote, index) in Math.ceil(result.vote_average/2)" :key="index" :icon="['fas', 'star']" />
          
                <font-awesome-icon v-for="unvote in Math.sign(5 - Math.ceil(result.vote_average/2))" :key="unvote+'x'" :icon="['far', 'star']" />

              </div>

            </div>

          </div>


        </div>

        </div>

    </main>
    
    <!-- <HeaderSite 
    :titleRequired="searchTitle" 
    :apiRequiredMovies="apiMovie"  
    :apiRequiredTvShow="seriesMovie" 
    @search="callApi()" 
    /> -->
    <!-- <MainSite :apiRequiredMovies="apiMovie"  :apiRequiredTvShow="seriesMovie"  :foundMovies="resultsFoundMovies"  :foundTvShow="resultsFoundTvShow" /> -->

  </div>
</template>

<script>
import axios from 'axios';

//import HeaderSite from './components/HeaderSite.vue'
//import MainSite from './components/MainSite.vue'


export default {
  name: 'App',

  /* components: {

    HeaderSite,
    //MainSite

  }, */

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

      flagUrl: 'https://flagcdn.com/16x12/',
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

    },

  },
}
</script>

<style lang="scss">

*{
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}

#app{
  background-color: rgb(20, 20, 20);
  width: 100%;
}

//Utility

.flex{
  display: flex;
}

.container{
  width: 80%;
  margin: auto;
  flex-wrap: wrap;
}

.col_3{
  width: calc(100% / 12 * 3);
  height: 430px;
  margin: 20px 35px;

  &:hover{
    
    img{
      display: none;
    }
    
    .info{
      display: block;
    }
  } 

}

.film img{
  width: 100%;
  height: 100%;
  display: block;
}


//header

header{
  height: 70px;
  padding: 0 35px;
  background-color: black;
  justify-content: space-between;
  align-items: center;
}

h1{
  color: rgb(229, 9, 20);
}

input{
  line-height: 1.5rem;
  padding: 0 13px;
  border: none;
  border-radius: 10px;
  background-color: rgb(20, 20, 20);
}

.search_start{
  font-size: 1.2rem;
  color: white;
  margin: 0 15px;
}


// Main

main{
  color: white;
}

.star{
  color: yellow;
}

.info{
  display: none;
}



</style>
