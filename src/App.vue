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
    <!-- /header -->



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


          <h2>TELEFILM</h2>

          <div class="container flex">

            <div v-for="result in resultsFoundTvShow" :key="result.id" class="tvshow col_3">
              
              <img :src="posterUrl + result.poster_path" alt="">

              <div class="info">

                <h3>{{result.name}}</h3>

                <h4>{{result.original_name}}</h4>

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
      

    },

    viewFlag(isoCode) {
      return this.flag.includes(isoCode)
    },


  },
}
</script>

<style lang="scss">

*{
  box-sizing: border-box;
  padding: 0;
  margin: 0;
  background-color: rgb(20, 20, 20);
}

#app{
  width: 100%;
}

//Utility

h1, h3, h4, p, span, img, .vote{
  background-color: black;
}

.flex{
  display: flex;
}

h2{
  text-align: center;
  margin: 75px 0 35px;
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
      width: 100%;
      height: 100%;
      padding: 25px;
      line-height: 1.5rem;
      display: block;
      background-color: black;

      h4{
        width: 100%;
        margin: 15px 0 35px;
      }

      .overview{
        width: 100%;
        height: 40%;
        overflow-y: auto;
      }

    }
  } 

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

.search_form{
   background-color: black;
}

input{
  line-height: 1.5rem;
  padding: 0 13px;
  background-color: white;
  border: none;
  border-radius: 10px;

  &:focus-visible{
    outline: none;
  }
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

img{
  width: 100%;
  height: 100%;
  display: block;
}

.info{
  display: none;
}


</style>
