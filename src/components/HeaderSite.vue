<template>
    <header id="site_header">

        <h1>BOOLFLIX</h1>

        <!-- componente di ricerca -->
        <div class="search">

            <input v-model="titleRequired" type="text" placeholder="Titolo">

            <button @click="callAPI()">
            Cerca
            </button>

        </div>

    </header>
</template>


<script>
export default {
    name: 'HeaderSite',

    data() {
        return {

        }
    },

    
}
</script>


<style lang="scss">

</style>