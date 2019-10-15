<template lang="pug">
  #app
    img(src='https://robertoocandom.github.io/Musiclafm/dist/logo2.png')
    h1 Platzi Music Curso
    select(v-model="selectedCountry")
      option(v-for="country in countries" v-bind:value="country.value") {{ country.name }}
    spinner(v-show="loading")
    ul
     artist(v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.mbid")
</template>

<script>
import Artist from './components/Artist.vue'
import getArtists from './api'
import Spinner from './components/Spinner.vue'

export default {
  name: 'app',
  data () {
    return {
      artists: [],
      countries: [
        {name: 'Argentina', value: 'argentina'},
        {name: 'Colombia', value: 'colombia'},
        {name: 'España', value: 'Spain'},
        {name: 'Venezuela', value: 'venezuela'}
      ],
      selectedCountry: 'argentina',
      loading: true
    }
  },
  components: 
  {
    Artist,
    Spinner
  },

  methods:{
    refreshArtists(){
      this.loading = true
      this.artists = []
      const self = this
      getArtists(this.selectedCountry)
        .then(function (artists) {
          self.loading = false
        self.artists = artists
        })
    }
  },
  mounted(){
    this.refreshArtists()
  },
  watch:{
    selectedCountry(){
      this.refreshArtists()
    }
  }
}
</script>

<style lang="stylus">
#app
  font-family 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50
  margin-top 60px


h1, h2
  font-weight normal


ul
  list-style-type none
  padding 0
  width 40%
  margin 0 auto 

li
  display inline-block
  margin 0 10px

a
  color #42b983


</style>
