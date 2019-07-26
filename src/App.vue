<template>
  <v-app class="app">
    <v-content>
      <v-layout justify-center row wrap fill-height>
        <v-flex xs12 md4 pa-4>
          <h2>My Top Rated Movies</h2>
          <ul>
            <li v-for="(m, index) in favoriteMovies" :key="index">{{m.title}}</li>
          </ul>
        </v-flex>
        <v-flex xs12 md8 pa-4 fill-height>
          <v-layout justify-left row wrap class="fill-height">
            <v-flex xs12>
              <h1>My Movies</h1>
            </v-flex>
            <v-flex xs6 sm4 md4 lg3 xl3 pa-2 v-for="(m, index) in movies" :key="index">
              <MovieCard @change-rating="m.rating=$event" :movie="m"></MovieCard>
            </v-flex>
          </v-layout>
        </v-flex>
      </v-layout>
    </v-content>
  </v-app>
</template>

<style scoped>
.app {
  padding: 1em;
}
</style>

<script>
import * as axios from "axios";
import MovieCard from "./components/MovieCard";

export default {
  name: "App",
  data: () => ({
    movies: []
  }),
  components: {
    MovieCard
  },
  methods: {
    getAllMovies: async function() {
      const url = "https://movie-api-test-page.herokuapp.com/api/movies";
      var res = [];
      await axios
        .get(url)
        .then(function(data) {
          res = data.data;
        })
        .catch(function(err) {
          // eslint-disable-next-line
          console.log(err);
        });
      return res;
    }
  },
  async created() {
    this.movies = await this.getAllMovies();
  },
  computed: {
    favoriteMovies: function() {
      return this.movies.filter(x => {
        return x.rating > 4;
      });
    }
  }
};
</script>
