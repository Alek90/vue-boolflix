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

  methods:{
    callAPI () {
      axios.get('https://api.themoviedb.org/3/search/movie?api_key=3d29c9625fadd02d13b86c0f4b58f8b7&language=en-US&page=1&query=jurassic&include_adult=false')
      .then((response) => {
        console.log((response.data.results));
      })
    }
  }
}
</script>

<style lang="scss">

</style>
