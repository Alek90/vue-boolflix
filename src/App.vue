<template>
  <div id="app">
    
    <HeaderSite :titleRequired="SearchTitle"/>
    <MainSite />

  </div>
</template>

<script>
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

      SearchTitle: '',
    }
  }

}
</script>

<style lang="scss">

</style>
