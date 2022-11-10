<template>
  <v-container>
    <v-row>
      <v-col cols="12" sm="4">
        <v-hover v-slot="{ hover }" open-delay="200">
          <v-card :elevation="hover ? 16 : 2" :class="{ 'on-hover': hover }">
            <v-img
              :src="'https://image.tmdb.org/t/p/w300/' + actor.profile_path"
              alt="actor"
            />
            <v-card-text>
              <v-row class="mx-0 d-flex justify-center">
                <v-btn
                  class="mx-2"
                  fab
                  dark
                  small
                  color="error"
                  :href="'https://facebook.com/' + socialDetails.facebook_id"
                >
                  <v-icon dark>fab fa-facebook-f </v-icon>
                </v-btn>
                <v-btn
                  class="mx-2"
                  fab
                  dark
                  small
                  color="error"
                  :href="'https://instagram.com/' + socialDetails.instagram_id"
                >
                  <v-icon dark> fab fa-instagram </v-icon>
                </v-btn>
                <v-btn
                  class="mx-2"
                  fab
                  dark
                  small
                  color="error"
                  :href="'https://twitter.com/' + socialDetails.twitter_id"
                >
                  <v-icon dark> fab fa-twitter </v-icon>
                </v-btn>
                <v-btn class="mx-2" fab dark small color="error">
                  <v-icon dark> fas fa-globe-asia </v-icon>
                </v-btn>
              </v-row>
            </v-card-text>
          </v-card>
        </v-hover>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      socialDetails: [],
      actor: {},
      knownFor: [],
      castMovies: {},
    };
  },
  mounted() {
    this.fetchActor(this.$route.params.id);
    this.fetchCredits(this.$route.params.id);
    this.fetchSocial(this.$route.params.id);
  },
  methods: {
    async fetchActor(actorId) {
      const response = await this.$http.get(
        "https://api.themoviedb.org/3/person/" + actorId
      );
      this.actor = response.data;
    },
    async fetchCredits(actorId) {
      const response = await this.$http.get(
        "https://api.themoviedb.org/3/person/" + actorId + "/combined_credits"
      );
      this.castMovies = response.data.cast;
      this.knownFor = response.data.cast
        .filter((x) => x.media_type == "movie")
        .slice(1, 6);
      /*this.knownFor = response.data.cast.slice(
        Math.max(response.data.cast.length - 5, 1)
      );*/
    },
    movieImage(movie) {
      const posterPath = movie.poster_path;
      if (!posterPath) {
        return "https://via.placeholder.com/185x278";
      }
      return "https://image.tmdb.org/t/p/w185/" + posterPath;
    },
    async fetchSocial(actorId) {
      const response = await this.$http.get(
        "https://api.themoviedb.org/3/person/" + actorId + "/external_ids"
      );
      this.socialDetails = response.data;
    },
    castDetails(cast) {
      return parseInt(cast.release_date) + " .";
    },
  },
};
</script>

<style></style>
