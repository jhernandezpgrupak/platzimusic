<template lang="pug">
  #app
    img(src='dist/logo.png')
    h1 PlatziMusic
    select(v-model="selectedcountry") 
      option(v-for="country in countries" v-bind:value="country.value") {{country.name}}
    spinner(v-show="loading")  
    ul
      artist(v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.mib")
      <!--li(v-for="artis in artists") {{artis.name }}-->


  <!--<div id="app">
    <img src="./assets/logo.png">
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <ul>
      <li><a href="https://vuejs.org" target="_blank">Core Docs</a></li>
      <li><a href="https://forum.vuejs.org" target="_blank">Forum</a></li>
      <li><a href="https://chat.vuejs.org" target="_blank">Community Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank">Twitter</a></li>
    </ul>
    <h2>Ecosystem</h2>
    <ul>
      <li><a href="http://router.vuejs.org/" target="_blank">vue-router</a></li>
      <li><a href="http://vuex.vuejs.org/" target="_blank">vuex</a></li>
      <li><a href="http://vue-loader.vuejs.org/" target="_blank">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank">awesome-vue</a></li>
    </ul>
  </div>-->
</template>

<script>
import Artist from './components/Artist.vue'
import getArtist from './api'
import Spinner from './components/Spinner.vue'
export default {
  name: 'app',
  data () {
    return {
      artists: [],
      countries:
      [
        {name: 'Mexico', value: 'mexico'},
        {name: 'España', value: 'spain'},
        {name: 'Colombia',  value: 'colombia'}
      ],
      selectedcountry:'mexico',
      loading:true
    }
  },
  components:
  {
    Artist,
    Spinner
  },
  methods: //Para llamarlo al cambiar el país
  {
    refreshArtist(){
      this.loading=true
      this.artists = []
      getArtist(this.selectedcountry)
      .then(artists => this.artists = artists)
      setTimeout(() => { this.loading=false }, 500);

    }
  }, 
  mounted()
  {
      this.refreshArtist() 
  },
  watch:
  {
      selectedcountry()
      {
        this.refreshArtist()
      }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
