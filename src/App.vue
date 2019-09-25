<template>
  <div id="app">
    <img src="./assets/logo.png" alt />
    <h1>PlatziMusic</h1>
    <select name id v-model="selectedCountry">
      <option v-for="(country,key) in countries" :value="country.value" :key="key">{{country.name}}</option>
    </select>
    <Spinner v-show="loading"></Spinner>
    <ul>
      <Artist v-for="artist in artists" :key="artist.mbi" :artist="artist"></Artist>
      <!-- <li>{{artist.name}}</li> -->
    </ul>
  </div>
</template>

<script>
import getArtists from "../api"; //no hace falta especificar el archivo index.js porque al llamarse index es el que va a requerir por defecto
import Artist from "./components/artists.vue";
import Spinner from "./components/Spinner.vue";
export default {
  name: "app",
  data() {
    return {
      artists: [],
      countries: [
        { name: "Colombia", value: "colombia" },
        { name: "Argentina", value: "argentina" },
        { name: "España", value: "spain" }
      ],
      selectedCountry: "colombia",
      loading: true
    };
  },
  components: {
    Artist,
    Spinner
  },
  methods: {
    refreshArtists() {
      this.loading = true;
      this.artists = [];
      getArtists(this.selectedCountry).then(artists => {
        console.log("artists", artists);
        this.loading = false;
        this.artists = artists;
      });
    }
  },
  mounted: function() {
    this.refreshArtists();
  },
  watch: {
    selectedCountry: function() {
      this.refreshArtists();
    }
  }
};
</script>

<style lang="stylus">
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
