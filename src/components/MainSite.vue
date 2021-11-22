<template>
    <main id="site_main">
       
        <!-- contenuto principale del #site_main -->
        <div class="results_found">

            <!-- film trovati -->
            <div class="films_found">

                

                <h2>FILM</h2>

                <div v-for="result in resultsFoundMovies" :key="result.id" class="film">

                    <h3>{{result.title}}</h3>

                    <p>{{result.original_title}}</p>

                    <country-flag :country= "result.original_language === 'en' ? 'gb' : result.original_language" size='big'/>

                    <div class="vote">

                        <p>{{Math.ceil(result.vote_average/2)}}</p>


                        <font-awesome-icon v-for="(vote, index) in Math.ceil(result.vote_average/2)" :key="index" :icon="['fas', 'star']" />
        
                        <font-awesome-icon v-for="unvote in Math.abs(5 - Math.ceil(result.vote_average/2))" :key="unvote+'x'" :icon="['far', 'star']" />

                    </div>

                    <img :src="posterUrl + result.poster_path" alt="">

                </div>

            </div>

            <!-- serie tv trovate -->
            <div class="tv_found">

                <h2>TELEFILM</h2>

                <div v-for="result in resultsFoundTvShow" :key="result.id" class="tvshow">

                    <h3>{{result.name}}</h3>

                    <p>{{result.original_name}}</p>

                    <country-flag country='result.original_language' size='big'/>

                    <div class="vote">

                        <p>{{Math.ceil(result.vote_average/2)}}</p>


                        <font-awesome-icon v-for="(vote, index) in Math.ceil(result.vote_average/2)" :key="index" :icon="['fas', 'star']" />
        
                        <font-awesome-icon v-for="unvote in Math.sign(5 - Math.ceil(result.vote_average/2))" :key="unvote+'x'" :icon="['far', 'star']" />

                    </div>

                    <img :src="posterUrl + result.poster_path" alt="">

                </div>

            </div>

        </div>

    </main>
</template>


<script>
//import axios from 'axios';

export default {
    name: 'MaineSite',

    props: {

        foundMovies: Object,

        foundTvShow: Object,

    },

    data() {

        return{

            //baseApiMovies: 'https://api.themoviedb.org/3/search/movie?api_key=3d29c9625fadd02d13b86c0f4b58f8b7&language=it-IT&page=1&include_adult=false&query=',

            //apiRequiredMovies: '',

            //resultsFoundMovies: '',

            //baseApiTvShow: 'https://api.themoviedb.org/3/search/tv?api_key=3d29c9625fadd02d13b86c0f4b58f8b7&language=it-IT&page=1&include_adult=false&query=',

            //apiRequiredTvShow: '',

            //resultsFoundTvShow: '',

            posterUrl: 'https://image.tmdb.org/t/p/w342',

            flagUrl: 'https://flagcdn.com/16x12/',
        }
    },

    methods:{

    /* creazione dell'API in apiRequiredMovies */
    /* createAPI(required) {
      this.apiRequiredMovies = this.baseApiMovies + required;
      this.apiRequiredTvShow = this.baseApiTvShow + required;
      // console.log(this.apiRequiredMovies); 
      // console.log(this.apiRequiredTvShow);
    }, */

    /* chiamata dell'API */
    /* callApi () {
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

    }, */

  }

}
</script>


<style lang="scss">

</style>


