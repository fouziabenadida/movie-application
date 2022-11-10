<template>
  <div class="mx-3">
    <h2 class="mt-2 grey--text">Popular Actors</h2>
    <v-container fluid>
      <v-row>
        <v-col cols="12" sm="3" v-for="actor in this.actors" :key="actor.id">
          <ActorCard :actor="actor" />
        </v-col>
        <v-col cols="12" class="d-flex justify-center mt-5">
          <v-btn
            class="mx-2"
            fab
            dark
            small
            color="error"
            v-on:click.prevent="previous()"
          >
            <v-icon dark> fas fa-step-backward </v-icon>
          </v-btn>
          <v-btn
            class="mx-2"
            fab
            dark
            small
            color="error"
            v-on:click.prevent="next()"
          >
            <v-icon dark> fas fa-step-forward </v-icon>
          </v-btn>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
let currentPage = 1;
import ActorCard from "../components/ActorCard.vue";
export default {
  name: "ActorsView",
  data() {
    return {
      actors: [],
    };
  },
  components: {
    ActorCard,
  },
  mounted() {
    this.fetchActors(currentPage);
  },
  methods: {
    async fetchActors(page) {
      try {
        const response = await this.$http.get(
          "https://api.themoviedb.org/3/person/popular?page=" + page
        );
        this.actors = response.data.results;
      } catch (error) {
        console.warn(error);
      }
    },
  },
  scroll() {
    window.onscroll = () => {
      let bottomOfWindow =
        document.documentElement.scrollTop + window.innerHeight ===
        document.documentElement.offsetHeight;
      if (bottomOfWindow) {
        currentPage += 1;
        this.fetchActors((currentPage += 1));
      }
    };
  },
};
</script>

<style></style>
